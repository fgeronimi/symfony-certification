---
title: PHP and Web Security - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# PHP and Web Security

## PHP API up to PHP 8.1 version

## Object Oriented Programming
- [Classes and Objects - php.net](http://php.net/manual/en/language.oop5.php)

À partir de PHP 8.0.0, les méthodes et propriétés peuvent aussi être accédés avec l'opérateur **"nullsafe": ?->.** L'opérateur nullsafe fonctionne à l'identique que l'accès de propriétés ou méthodes comme si dessus, à l'exception que si l'objet qui est déréférencé est null alors null sera retourné au lieu de lancer une exception. Si le déréférencement fait par d'une chaîne, le reste de la chaîne est ignoré.

L'opérateur nullsafe est mieux utilisé quand null est considéré une valeur valide et potentiellement attendu pour une propriété ou valeur de retour d'une méthode. Pour indiquer une erreur, une exception lancé est préférable.

**Les constantes de classes peuvent être redéfinies par une classe enfant.**

Le constructeur peut être rendu privé ou protégé pour empêcher son appel depuis l'extérieur. Dans ce cas, seul une méthode statique sera capable d'instancier la classe. Car elles sont dans la même définition de classe elles ont accès aux méthodes privées, même dans une instance différente de l'objet. Un constructeur privé est optionnel et peut ou pas faire de sens en fonction du cas d'utilisation.


Les méthodes suivantes sont considérées magiques : 
- __construct(), 
- __destruct(), 
- __call(), 
- __callStatic(), 
- __get(), 
- __set(), 
- __isset(), 
- __unset(), 
- __sleep(), 
- __wakeup(), 
- __serialize(), 
- __unserialize(), 
- __toString(), 
- __invoke(), 
- __set_state(), 
- __clone(), 
- __debugInfo().

Avertissement
Toutes les méthodes magiques, à l'exception de __construct(), __destruct(), et __clone(), doivent être déclaré en tant que public, sinon une E_WARNING est émise. Antérieur à PHP 8.0.0, aucun diagnostic n'était émis pour les méthodes magiques __sleep(), __wakeup(), __serialize(), __unserialize(), et __set_state().
Avertissement
Si des déclarations de types sont utilisé dans la définition d'une méthode magique, elles doivent être identique à la signature décrit dans ce document. Sinon, une erreur fatale est émise. Antérieur à PHP 8.0.0, aucun diagnostic n'était émis. Cependant, __construct() et __destruct() ne doivent pas déclarer un type de retour ; sinon une erreur fatale est émise.

## Namespaces
- [PHP Namespaces in 120 seconds - symfonycasts.com](https://symfonycasts.com/screencast/php-namespaces-in-120-seconds)
- [Namespaces - php.net](http://php.net/manual/en/language.namespaces.php)

## Interfaces
- [Object Interfaces - php.net](http://php.net/manual/en/language.oop5.interfaces.php)
- [Type Operators - php.net](http://php.net/manual/en/language.operators.type.php)
- [Type declarations - php.net](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)

## Anonymous functions and closures
- [Anonymous functions - php.net](http://php.net/manual/en/functions.anonymous.php)

Les fonctions anonymes, aussi appelées fermetures ou closures permettent la création de fonctions sans préciser leur nom. Elles sont particulièrement utiles comme fonctions de rappel callable, mais leur utilisation n'est pas limitée à ce seul usage.

Les fonctions anonymes sont implémentées en utilisant la classe Closure.

Lorsque déclarée dans le contexte d'une classe, la classe courante est automatiquement liée, la rendant $this disponible dans le contexte de la fonction. Si ce liage automatique de la classe courante n'est pas souhaité, alors les fonctions anonymes statiques peuvent être utilisées à la place.

- [Closure - php.net](http://php.net/manual/en/class.closure.php)

Closure::__construct — Constructeur empêchant l'instanciation  
Closure::bind — Duplique une fermeture avec un nouvel objet lié et un nouveau contexte de classe.  
Closure::bindTo — Duplique la fermeture avec un nouvel objet lié et un nouveau contexte de classe.   
Closure::call — Lie et appelle la fermeture  
Closure::fromCallable — Convertis un callable en une fermeture  

## Abstract classes
- [Class Abstraction - php.net](http://php.net/manual/en/language.oop5.abstract.php)

## Exception and error handling
- [Exception (class) - php.net](http://php.net/manual/en/class.exception.php)
- [Exceptions - php.net](http://php.net/manual/fr/language.exceptions.php)

## Traits
- [Traits - php.net](http://php.net/manual/fr/language.oop5.traits.php)

Une méthode héritée depuis une **classe mère est écrasée par une méthode issue d'un Trait**. L'ordre de précédence fait en sorte que **les méthodes de la classe courante écrasent les méthodes issues d'un Trait**, elles-mêmes surchargeant les méthodes héritées.

## PHP extensions
- [Extensions (sorted by Membership) - php.net](http://php.net/manual/en/extensions.membership.php)

- Arrays
- Classes/Objects
- CSPRNG
- Date/Time
- Directories
- Error Handling
- Program execution
- Filesystem
- FastCGI Process Manager
- Function Handling
- Hash
- PHP Options/Info
- JSON
- Mail
- Math
- Misc.
- Network
- OPcache
- Output Control
- Password Hashing
- PCRE
- Reflection
- SPL
- Streams
- Strings
- URLs
- Variable handling

## SPL
- [Standard PHP Library - php.net](http://php.net/book.spl)

La bibliothèque standard PHP (SPL) est une collection d'interfaces et de classes qui ont été créées afin de résoudre les problèmes communs.

SPL fournit des structures de données, un ensemble d'itérateur pour traverser des objets, des interfaces, un ensemble d'exceptions standards ainsi qu'un certain nombre de classes pour travailler avec des fichiers. SPL fournit aussi un jeu de fonctions telle que spl_autoload_register().

La classe **SplDoublyLinkedList** fournit l'interface principale pour les listes doublement chaînées.
- SplDoublyLinkedList. 
- SplStack. 
- SplQueue. 

Les tas sont des structures de type arbre, qui suivent une propriété caractéristique : **chaque nœud est plus grand ou égal que ses enfants**, lorsqu'on les compare avec la méthode implémentée de comparaison, qui est globale au tas.

- SplHeap. 
- SplMaxHeap. 
- SplMinHeap. 
- SplPriorityQueue. 

La classe **SplFixedArray** fournit les fonctionnalités principales d'un **tableau**. La différence majeure entre un objet SplFixedArray et un tableau standard de PHP est que **SplFixedArray doit être redimensionné manuellement, et n'utilise que des entier dans cette intervale pour les index. L'avantage est qu'il utilise moins de mémoire qu'un tableau standard.**

La classe **SplObjectStorage** fournit une carte d'objets ou de données, ou encore, en ignorant les index, un ensemble d'objets. Ce double objectif est utile dans de nombreuses situations, où il faut identifier de manière unique des objets.

