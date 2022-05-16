---
title: Data Validation - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Data Validation
- [Validation - symfony.com](https://symfony.com/doc/6.0/validation.html)

## PHP object validation
- [The Basics of Validation - symfony.com](https://symfony.com/doc/6.0/validation.html#the-basics-of-validation)

## Built-in validation constraints
- [Supported Constraints - symfony.com](https://symfony.com/doc/5.0/validation.html#supported-constraints)

**Basic Constraints**  
```
NotBlank
Blank
NotNull
IsNull
IsTrue
IsFalse
Type
```
**String Constraints**
```
Email
ExpressionLanguageSyntax
Length
Url
Regex
Hostname
Ip
Cidr
Json
Uuid
Ulid
UserPassword
NotCompromisedPassword  
CssColor  
```
**Comparison Constraints**
```
EqualTo  
NotEqualTo  
IdenticalTo  
NotIdenticalTo  
LessThan  
LessThanOrEqual  
GreaterThan  
GreaterThanOrEqual  
Range  
DivisibleBy  
Unique  
```
**Number Constraints**
```
Positive  
PositiveOrZero  
Negative  
NegativeOrZero  
Date Constraints  
Date  
DateTime  
Time  
Timezone  
```
**Choice Constraints**
```
Choice  
Language  
Locale  
Country  
```
**File Constraints**  
```
File  
Image  
```
**Financial and other Number Constraints**
```
Bic  
CardScheme  
Currency  
Luhn  
Iban  
Isbn  
Issn  
Isin  
```
**Other Constraints**
```
AtLeastOneOf  
Sequentially
Compound  
Callback  
Expression  
All  
Valid  
Traverse  
Collection  
Count  
UniqueEntity  
```

## Validation scopes
- [Constraint Targets - symfony.com](https://symfony.com/doc/6.0/validation.html#constraint-targets)

### Properties

```
// src/Entity/Author.php

// ...
use Symfony\Component\Validator\Constraints as Assert;

class Author
{
    /**
     * @Assert\NotBlank
     * @Assert\Length(min=3)
     */
    private $firstName;
}
```

### Getters
Constraints can also be applied to the return value of a method. Symfony allows you to add a constraint to any public method **whose name starts with "get", "is" or "has"**. In this guide, these types of methods are referred to as "getters".

```
// src/Entity/Author.php
namespace App\Entity;

// ...
use Symfony\Component\Validator\Constraints as Assert;

class Author
{
    /**
     * @Assert\IsTrue(message="The password cannot match your first name")
     */
    public function isPasswordSafe()
    {
        return $this->firstName !== $this->password;
    }
}
```


## Validation groups
- [How to Apply only a Subset of all Your Validation Constraints (Validation Groups) - symfony.com](https://symfony.com/doc/6.0/validation/groups.html)
```
// src/Entity/User.php
namespace App\Entity;

use Symfony\Component\Security\Core\User\UserInterface;
use Symfony\Component\Validator\Constraints as Assert;

class User implements UserInterface
{
    /**
     * @Assert\Email(groups={"registration"})
     */
    private $email;

    /**
     * @Assert\NotBlank(groups={"registration"})
     * @Assert\Length(min=7, groups={"registration"})
     */
    private $password;

    /**
     * @Assert\Length(min=2)
     */
    private $city;
}
```
With this configuration, there are three validation groups:

- **Default :**  Contains the constraints in the current class and **all referenced classes that belong to no other group**. In this example, it only contains the city field.
- **User :**  Equivalent to **all constraints of the User object in the Default group**. This is always the name of the class. The difference between this and Default is explained later
- **registration :** This is a **custom validation group**, so it only contains the constraints that are explicitly associated with it. In this example, only the email and password fields.

Constraints in the Default group of a class are the constraints that have either no explicit group configured or that are configured to a group equal to the class name or the string Default.

When validating *just* the User object, there is no difference between the Default group and the User group. 
But, there is a difference if User has embedded objects. For example, imagine User has an address property that contains some Address object and that you've added the Valid constraint to this property so that it's validated when you validate the User object.

If you validate User using the Default group, then any constraints on the Address class that are in the Default group *will* be used.
But, **if you validate User using the User validation group, then only constraints on the Address class with the User group will be validated.**

In other words, the Default group and the class name group (e.g. User) are identical, **except when the class is embedded in another object that's actually the one being validated.**

If you have inheritance (e.g. User extends BaseUser) and you validate with the class name of the subclass (i.e. User), then all constraints in the User and BaseUser will be validated. However, if you validate using the base class (i.e. BaseUser), then only the default constraints in the BaseUser class will be validated.

To tell the validator to use a specific group, pass one or more group names as the third argument to the validate() method::
```
$errors = $validator->validate($author, null, ['registration']);
```
If no groups are specified, all constraints that belong to the group Default will be applied.


## Group sequence
- [How to Sequentially Apply Validation Groups - symfony.com](https://symfony.com/doc/6.0/validation/sequence_provider.html)

In this example, it will first validate all constraints in the group User (which is the same as the Default group). Only if all constraints in that group are valid, the second group, Strict, will be validated. :
```
// src/Entity/User.php
namespace App\Entity;

use Symfony\Component\Security\Core\User\UserInterface;
use Symfony\Component\Validator\Constraints as Assert;

/**
 * @Assert\GroupSequence({"User", "Strict"})
 */
class User implements UserInterface
{
    /**
     * @Assert\NotBlank
     */
    private $username;

    /**
     * @Assert\NotBlank
     */
    private $password;

    /**
     * @Assert\IsTrue(message="The password cannot match your username", groups={"Strict"})
     */
    public function isPasswordSafe()
    {
        return ($this->username !== $this->password);
    }
}
```

You can also define a group sequence in the validation_groups form option:

```
class MyType extends AbstractType
{
    // ...
    public function configureOptions(OptionsResolver $resolver)
    {
        $resolver->setDefaults([
            'validation_groups' => new GroupSequence(['First', 'Second']),
        ]);
    }
}

```

```
// src/Entity/User.php
namespace App\Entity;

// ...
use Symfony\Component\Validator\GroupSequenceProviderInterface;

/**
 * @Assert\GroupSequenceProvider
 */
class User implements GroupSequenceProviderInterface
{
    // ...

    public function getGroupSequence()
    {
        // when returning a simple array, if there's a violation in any group
        // the rest of the groups are not validated. E.g. if 'User' fails,
        // 'Premium' and 'Api' are not validated:
        return ['User', 'Premium', 'Api'];

        // when returning a nested array, all the groups included in each array
        // are validated. E.g. if 'User' fails, 'Premium' is also validated
        // (and you'll get its violations too) but 'Api' won't be validated:
        return [['User', 'Premium'], 'Api'];
    }
}
```

Sometimes, you may want to apply constraints sequentially on a single property. The Sequentially constraint can solve this for you in a more straightforward way than using a GroupSequence.

## Custom callback validators
- [Callback Constraint - symfony.com](https://symfony.com/doc/6.0/reference/constraints/Callback.html)
```
// ...
use Symfony\Component\Validator\Context\ExecutionContextInterface;

class Author
{
    // ...
    private $firstName;
    
    /**
     * @Assert\Callback
     */
    public function validate(ExecutionContextInterface $context, $payload)
    {
        // somehow you have an array of "fake names"
        $fakeNames = [/* ... */];

        // check if the name is actually a fake name
        if (in_array($this->getFirstName(), $fakeNames)) {
            $context->buildViolation('This name sounds totally fake!')
                ->atPath('firstName')
                ->addViolation();
        }
    }
}
```
## Violations builder
- [Custom Validation Constraint - symfony.com](https://symfony.com/doc/6.0/validation/custom_constraint.html)
