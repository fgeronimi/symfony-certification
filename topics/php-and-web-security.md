---
title: PHP and Web Security - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# PHP and Web Security

## PHP API up to PHP 7.2 version

## Object Oriented Programming
- [Classes and Objects - php.net](http://php.net/manual/en/language.oop5.php)

À partir de PHP 8.0.0, les méthodes et propriétés peuvent aussi être accédés avec l'opérateur "nullsafe": ?->. L'opérateur nullsafe fonctionne à l'identique que l'accès de propriétés ou méthodes comme si dessus, à l'exception que si l'objet qui est déréférencé est null alors null sera retourné au lieu de lancer une exception. Si le déréférencement fait par d'une chaîne, le reste de la chaîne est ignoré.

Note:
L'opérateur nullsafe est mieux utilisé quand null est considéré une valeur valide et potentiellement attendu pour une propriété ou valeur de retour d'une méthode. Pour indiquer une erreur, une exception lancé est préférable.

Note:
Les constantes de classes peuvent être redéfinies par une classe enfant.

Le constructeur peut être rendu privé ou protégé pour empêcher son appel depuis l'extérieur. Dans ce cas, seul une méthode statique sera capable d'instancier la classe. Car elles sont dans la même définition de classe elles ont accès aux méthodes privées, même dans une instance différente de l'objet. Un constructeur privé est optionnel et peut ou pas faire de sens en fonction du cas d'utilisation.

## Namespaces
- [PHP Namespaces in 120 seconds - symfonycasts.com](https://symfonycasts.com/screencast/php-namespaces-in-120-seconds)
- [Namespaces - php.net](http://php.net/manual/en/language.namespaces.php)

## Interfaces
- [Object Interfaces - php.net](http://php.net/manual/en/language.oop5.interfaces.php)
- [Type Operators - php.net](http://php.net/manual/en/language.operators.type.php)
- [Type declarations - php.net](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)

## Anonymous functions and closures
- [Anonymous functions - php.net](http://php.net/manual/en/functions.anonymous.php)
- [Closure - php.net](http://php.net/manual/en/class.closure.php)

## Abstract classes
- [Class Abstraction - php.net](http://php.net/manual/en/language.oop5.abstract.php)

## Exception and error handling
- [Exception (class) - php.net](http://php.net/manual/en/class.exception.php)
- [Exceptions - php.net](http://php.net/manual/en/language.exceptions.php)

## Traits
- [Traits - php.net](http://php.net/manual/en/language.oop5.traits.php)

## PHP extensions
- [Extensions (sorted by Membership) - php.net](http://php.net/manual/en/extensions.membership.php)

## SPL
- [Standard PHP Library - php.net](http://php.net/book.spl)
