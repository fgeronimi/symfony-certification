---
title: Symfony Architecture - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Symfony Architecture

## Symfony Flex
- [Symfony 5.0 Documentation - symfony.com](https://symfony.com/doc/5.0/index.html)
- [Using Symfony Flex to Manage Symfony Applications - symfony.com](https://symfony.com/doc/6.0/setup/flex.html)
```
composer require symfony/flex
```
Symfony Flex recommends that applications use the following directory structure :
```
your-project/
├── assets/
├── bin/
│   └── console
├── config/
│   ├── bundles.php
│   ├── packages/
│   ├── routes.yaml
│   └── services.yaml
├── public/
│   └── index.php
├── src/
│   ├── ...
│   └── Kernel.php
├── templates/
├── tests/
├── translations/
├── var/
└── vendor/
```

## License
- [Symfony License - symfony.com](https://symfony.com/doc/6.0/contributing/code/license.html)

## Components
- [Symfony Components - symfony.com](https://symfony.com/components)
```
composer require symfony/xxxxxx 
```
**Base :**
- **symfony/asset** : Manages URL generation and versioning of web assets such as CSS stylesheets, JavaScript files and image files.  
- **symfony/browser-kit** : Simulates the behavior of a web browser.
- **symfony/cache** : Implements PSR-6 and PSR-16 caching mechanisms and provides adapters for popular caching backends (Redis, Memcache, APCu, etc.)  
- **symfony/config** : Helps you find, load, combine, autofill and validate configuration values.  
- **symfony/console** : Eases the creation of beautiful and testable command line interfaces.  
- symfony/contracts : A set of abstractions extracted out of the Symfony components.  
- symfony/crowdin-translation-provider : Provides Crowdin integration for Symfony Translation.  
- symfony/css-selector : Converts CSS selectors to XPath expressions.  
- **symfony/dependency-injection** : Allows you to standardize and centralize the way objects are constructed in your application.  
- **symfony/dom-crawler** : Eases DOM navigation for **HTML and XML documents**.  
- **symfony/dotenv** : Parses .env files to make environment variables stored in them accessible via **getenv(), $_ENV or $_SERVER**.  
- **symfony/error-handler** : Provides tools to manage errors and ease debugging PHP code.  
- **symfony/event-dispatcher** : Implements the **Mediator pattern** in a simple and effective way to make projects truly extensible.  
- **symfony/expression-language** : Provides an engine that can compile and evaluate expressions.  
- **symfony/filesystem** : Provides basic utilities for the filesystem.  
- **symfony/finder** : Finds files and directories via an intuitive fluent interface.  
- **symfony/form** : Provides tools to easy creating, processing and reusing HTML forms.  
- symfony/security-guard : Brings many layers of authentication together, making it much easier to create complex authentication systems where you have total control.  
- **symfony/http-client** : A low-level HTTP client with support for both **PHP stream wrappers and cURL**. It also provides utilities **to consume APIs**.  
- **symfony/http-foundation** : Defines an object-oriented layer for the HTTP specification.  
- **symfony/http-kernel** : Provides the building blocks to create flexible and fast HTTP-based frameworks.  
- symfony/intl : Provides fallback code to handle cases when the intl extension is missing.  
- **symfony/ldap** : Provides an LDAP client for PHP on top of PHP's ldap extension.  
- **symfony/lock** : Creates and manages locks, a **mechanism to provide exclusive access to a shared resource**.  
- symfony/loco-translation-provider : Provides Loco integration for Symfony Translation.  
- symfony/lokalise-translation-provider : Provides Lokalise integration for Symfony Translation.  
- **symfony/messenger** : Helps applications **send and receive messages to/from other applications or via message queues**.  
- symfony/mime : Allows manipulating MIME messages, used to create advanced email messages.  
- **symfony/options-resolver** : Helps you configuring objects with **option arrays**.  
- **symfony/phpunit-bridge** : Provides utilities to report legacy tests and usage of deprecated code and a helper for time-sensitive tests.  
- **symfony/password-hasher : Provides secure password hashing utilities.  
- symfony/process : Executes commands in sub-processes.  
- **symfony/property-access** : Provides function to read and write from/to an object or array using a simple string notation.  
- **symfony/property-info** : Extracts information about the properties of PHP classes using **metadata of popular sources** (Doctrine, PHP Reflection, PHPdoc, etc.)  
- **symfony/rate-limiter** : Provides a **Token Bucket implementation** to rate limit input and output in your application (e.g. to implement login throttling).  
- **symfony/routing** : Maps an HTTP request to a set of configuration variables.  
- symfony/runtime : Decouples the bootstrapping logic from any global state to make sure the application can run with runtimes like PHP-FPM, ReactPHP, Swoole, etc. without any changes.  
- **symfony/security** : Provides an infrastructure for sophisticated authorization systems.  
- **symfony/semaphore** : Creates and manages semaphores, a mechanism to control access to a **common resource by multiple processes** in a **concurrent system**.  
- **symfony/serializer** : Turns objects into a **specific format (XML, JSON, Yaml, ...) and the other way around**.  
- **symfony/stopwatch** : Provides a way to profile code.  
- **symfony/string** : Provides an object-oriented API to strings and deals with bytes, UTF-8 code points and grapheme clusters in a unified way. It also provides a **slugger** and an **inflector**.  
- symfony/templating : Provides all the tools needed to build any kind of template system.  
- **symfony/translation** : Provides tools to internationalize your application.  
- **symfony/uid** : Provides tools to work with unique identifiers such as **UUIDs and ULIDs**.  
- **symfony/validator** : Provides tools to validate classes.  
- **symfony/var-dumper** : Provides mechanisms for walking through any arbitrary PHP variable.  
- symfony/var-exporter : Exports any serializable PHP data structure to plain PHP code and allows to instantiate and populate objects without calling their constructors.  
- symfony/web-link : Implements HTML5 Links, Preload and Resource Hints specifications to advise clients (browsers) to preload and prefetch documents through HTTP and HTTP/2 pushes.  
- symfony/webpack-encore : symfony/webpack-encore  
- **symfony/workflow** : Provides tools for managing a **workflow** or **finite state machine**.  
- **symfony/yaml** : Loads and dumps YAML files.  

**Mailer :**
- **symfony/mailer** : Helps sending emails and provides integration with the most popular mailing services.  
- symfony/amazon-mailer : Provides Amazon SES integration for Symfony Mailer.
- symfony/google-mailer : symfony/google-mailer  
- symfony/mailchimp-mailer : symfony/mailchimp-mailer  
- symfony/mailgun-mailer : symfony/mailgun-mailer  
- symfony/mailjet-mailer : symfony/mailjet-mailer  
- symfony/oh-my-smtp-mailer : symfony/oh-my-smtp-mailer  
- symfony/postmark-mailer : symfony/postmark-mailer  
- symfony/sendgrid-mailer : Provides Sendgrid integration for Symfony Mailer.  
- symfony/sendinblue-mailer : symfony/sendinblue-mailer  

**Notifier :**
- **symfony/notifier** : Sends notifications via one or more channels (email, SMS, Slack, Telegram, ...)  
- symfony/all-my-sms-notifier : symfony/all-my-sms-notifier  
- symfony/amazon-sns-notifier : symfony/amazon-sns-notifier  
- symfony/clickatell-notifier : symfony/clickatell-notifier  
- symfony/discord-notifier : symfony/discord-notifier  
- symfony/esendex-notifier : symfony/esendex-notifier  
- symfony/fake-chat-notifier : Provides Fake Chat integration for Symfony Notifier. 
- symfony/fake-sms-notifier : Provides Fake SMS integration for Symfony Notifier.  
- symfony/firebase-notifier : symfony/firebase-notifier  
- symfony/free-mobile-notifier : symfony/free-mobile-notifier  
- symfony/gateway-api-notifier : symfony/gateway-api-notifier  
- symfony/gitter-notifier : symfony/gitter-notifier  
- symfony/google-chat-notifier : symfony/google-chat-notifier  
- symfony/infobip-notifier : symfony/infobip-notifier  
- symfony/iqsms-notifier : symfony/iqsms-notifier  
- symfony/light-sms-notifier : symfony/light-sms-notifier  
- symfony/linked-in-notifier : symfony/linked-in-notifier  
- symfony/mailjet-notifier : symfony/mailjet-notifier  
- symfony/mattermost-notifier : symfony/mattermost-notifier  
- symfony/mercure-notifier : symfony/mercure-notifier  
- symfony/message-bird-notifier : symfony/message-bird-notifier  
- symfony/message-media-notifier : symfony/message-media-notifier  
- symfony/microsoft-teams-notifier : symfony/microsoft-teams-notifier  
- symfony/mobyt-notifier : symfony/mobyt-notifier  
- symfony/nexmo-notifier : symfony/nexmo-notifier  
- symfony/octopush-notifier : symfony/octopush-notifier  
- symfony/ovh-cloud-notifier : symfony/ovh-cloud-notifier 
- symfony/rocket-chat-notifier : symfony/rocket-chat-notifier  
- symfony/smsapi-notifier : symfony/smsapi-notifier  
- symfony/smsc-notifier : symfony/smsc-notifier  
- symfony/sendinblue-notifier : symfony/sendinblue-notifier 
- symfony/sinch-notifier : symfony/sinch-notifier  
- symfony/slack-notifier : symfony/slack-notifier  
- symfony/sms-biuras-notifier : symfony/sms-biuras-notifier  
- symfony/spot-hit-notifier : symfony/spot-hit-notifier  
- symfony/telegram-notifier : symfony/telegram-notifier  
- symfony/telnyx-notifier : symfony/telnyx-notifier  
- symfony/turbo-sms-notifier : symfony/turbo-sms-notifier  
- symfony/twilio-notifier : symfony/twilio-notifier  
- symfony/yunpian-notifier : symfony/yunpian-notifier  
- symfony/zulip-notifier : symfony/zulip-notifier  

**Polyfill :**  
- symfony/polyfill-apcu : symfony/polyfill-apcu  
- symfony/polyfill-ctype : symfony/polyfill-ctype  
- symfony/polyfill-iconv : symfony/polyfill-iconv  
- symfony/polyfill-intl-grapheme : symfony/polyfill-intl-grapheme  
- symfony/polyfill-intl-icu : symfony/polyfill-intl-icu  
- symfony/polyfill-intl-idn : symfony/polyfill-intl-idn  
- symfony/polyfill-intl-messageformatter : symfony/polyfill-intl-messageformatter  
- symfony/polyfill-intl-normalizer : symfony/polyfill-intl-normalizer  
- symfony/polyfill-mbstring : Provides a partial, native PHP implementation for the Mbstring extension.    
- symfony/polyfill-php54 : symfony/polyfill-php54  
- symfony/polyfill-php55 : symfony/polyfill-php55  
- symfony/polyfill-php56 : symfony/polyfill-php56  
- symfony/polyfill-php70 : symfony/polyfill-php70  
- symfony/polyfill-php71 : symfony/polyfill-php71  
- symfony/polyfill-php72 : symfony/polyfill-php72  
- symfony/polyfill-php73 : symfony/polyfill-php73  
- symfony/polyfill-php74 : symfony/polyfill-php74  
- symfony/polyfill-php80 : symfony/polyfill-php80  
- symfony/polyfill-php81 : symfony/polyfill-php81  
- symfony/polyfill-uuid : symfony/polyfill-uuid  
- symfony/polyfill-util : symfony/polyfill-util  
  






## Bridges
- [What are symfony bridges, bundles and vendor? - stackoverflow.com](https://stackoverflow.com/questions/11888522/what-are-symfony-bridges-bundles-and-vendor)

## Code organization
- [Organizing Your Business Logic - symfony.com](https://symfony.com/doc/6.0/best_practices/business-logic.html)

## Request handling
- [Symfony and HTTP Fundamentals - symfony.com](https://symfony.com/doc/6.0/introduction/http_fundamentals.html)

## Exception handling
- [How to Customize Error Pages - symfony.com](https://symfony.com/doc/5.0/controller/error_pages.html)

## Event dispatcher and kernel events
- [Symfony Framework Events - symfony.com](https://symfony.com/doc/5.0/reference/events.html)
- [The HttpKernel Component - symfony.com](https://symfony.com/doc/5.0/components/http_kernel.html)
- [The EventDispatcher Component - symfony.com](https://symfony.com/doc/5.0/components/event_dispatcher.html)

## Official best practices
- [Symfony Best Practices - symfony.com](https://symfony.com/doc/5.0/best_practices/index.html)

## Release management
- [The Release Process - symfony.com](https://symfony.com/doc/5.0/contributing/community/releases.html)

## Backward compatibility promise
- [Our Backwards Compatibility Promise - symfony.com](https://symfony.com/doc/5.0/contributing/code/bc.html)

## Deprecations best practices
- [Deprecations - symfony.com](https://symfony.com/doc/5.0/contributing/code/conventions.html#deprecations)

## Framework overloading

## Release management and roadmap schedule
- [Symfony Roadmap - symfony.com](https://symfony.com/roadmap)
- [The Release Process - symfony.com](https://symfony.com/doc/5.0/contributing/community/releases.html)

## Framework interoperability and PSRs
- [Six good reasons to use Symfony - #6 Interoperability - symfony.com](https://symfony.com/six-good-reasons)
- [Coding Standards - symfony.com](https://symfony.com/doc/5.0/contributing/code/standards.html)
- [PSR-1: Basic Coding Standard - php-fig.org](http://www.php-fig.org/psr/psr-1/)
- [PSR-2: Coding Style Guide - php-fig.org](http://www.php-fig.org/psr/psr-2/)
- [PSR-4: Autoloader - php-fig.org](http://www.php-fig.org/psr/psr-4/)

## Naming conventions
- [Method Names - symfony.com](https://symfony.com/doc/5.0/contributing/code/conventions.html#method-names)
