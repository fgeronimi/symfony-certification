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
- [How to Sequentially Apply Validation Groups - symfony.com](https://symfony.com/doc/5.0/validation/sequence_provider.html)

## Custom callback validators
- [Callback Constraint - symfony.com](https://symfony.com/doc/5.0/reference/constraints/Callback.html)

## Violations builder
- [Custom Validation Constraint - symfony.com](https://symfony.com/doc/5.0/validation/custom_constraint.html)
