---
title: Symfony Architecture - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Symfony Architecture

## Symfony Flex
- [Symfony 6.0 Documentation - symfony.com](https://symfony.com/doc/6.0/index.html)
- [Using Symfony Flex to Manage Symfony Applications - symfony.com](https://symfony.com/doc/6.0/setup/flex.html)
- [Symfony Recipe - github.com](https://github.com/symfony/recipes)
```
composer require symfony/flex
```
From a technical point of view, Symfony Flex is just a **Composer plugin**. It hooks on Composer events whenever you run a command that installs, updates or removes a PHP package or Symfony bundle.

Flex will take care of registering the bundle in the **Symfony kernel**, providing **a default configuration**, loading the **necessary routes**, **etc.**  

For exemple, the single Composer command ```composer require api-platform``` will have been enough for you to set up a functional REST API and its swagger/openapi documentation.

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
- [How to Customize Error Pages - symfony.com](https://symfony.com/doc/6.0/controller/error_pages.html)

Error pages for the production environment can be customized in different ways depending on your needs:  

If you only want to change **the contents and styles of the error pages to match the rest of your application**, override the **default error templates**;  
If you want to change the **contents of non-HTML error output**, create a **new normalizer;**  
If you also want to **tweak the logic used by Symfony to generate error pages**, override **the default error controller;**  
If you need total control of **exception handling to run your own logic** use the **kernel.exception event**.  


## Event dispatcher and kernel events
- [Symfony Framework Events - symfony.com](https://symfony.com/doc/6.0/reference/events.html)
- [The HttpKernel Component - symfony.com](https://symfony.com/doc/6.0/components/http_kernel.html)
- [The EventDispatcher Component - symfony.com](https://symfony.com/doc/6.0/components/event_dispatcher.html)



**Kernel Events :**


|Name   |KernelEvents Constant  | Argument passed to the listener  |
|---|---|---|
|kernel.request|	KernelEvents::REQUEST|	RequestEvent|
|kernel.controller	|KernelEvents::CONTROLLER	|ControllerEvent|
|kernel.controller_arguments|	KernelEvents::CONTROLLER_ARGUMENTS|	ControllerArgumentsEvent|
|kernel.view	|KernelEvents::VIEW|	ViewEvent|
|kernel.response	|KernelEvents::RESPONSE	|ResponseEvent|
|kernel.finish_request|	KernelEvents::FINISH_REQUEST|	FinishRequestEvent|
|kernel.terminate|	KernelEvents::TERMINATE|	TerminateEvent|
|kernel.exception|	KernelEvents::EXCEPTION|	ExceptionEvent|

Execute this command to find out which listeners are registered for this event and their priorities:
```
php bin/console debug:event-dispatcher kernel.xxxxv
```

**The Workflow of a Request :**  

Every HTTP web interaction begins with a request and ends with a response. Your job as a developer is to create PHP code that reads the request information (e.g. the URL) and creates and returns a response (e.g. an HTML page or JSON string). This is a simplified overview of the request workflow in Symfony applications:  

- The user asks for a resource in a browser;
- The browser sends a request to the server;
- Symfony gives the application a Request object;
- The application generates a Response object using the data of the Request object;
- The server sends back the response to the browser;
- The browser displays the resource to the user.

Internally, ```HttpKernel::handle()``` - the concrete implementation of ```HttpKernelInterface::handle()``` - defines a **workflow** that starts with a **Request** and ends with a **Response**.

![http_kernel](https://symfony.com/doc/current/_images/components/http_kernel/http-workflow.svg)

The exact details of this workflow are the key to understanding how the kernel (and the Symfony Framework or any other library that uses the kernel) works.

1) The kernel.request Event
2) Resolve the Controller
3) The kernel.controller Event
4) Getting the Controller Arguments
5) Calling the Controller
6) The kernel.view Event
7) The kernel.response Event
8) The kernel.terminate Event
Handling Exceptions: the kernel.exception Event


**Sub Requests :**  

In addition to the "main" request that's sent into HttpKernel::handle(), you can also send a so-called "sub request". A sub request looks and acts like any other request, but typically serves to render just one small portion of a page instead of a full page. You'll most commonly make sub-requests from your controller (or perhaps from inside a template, that's being rendered by your controller).

To execute a sub request, use HttpKernel::handle(), but **change the second argument** as follows:

```
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpKernel\HttpKernelInterface;

// ...

// create some other request manually as needed
$request = new Request();
// for example, possibly set its _controller manually
$request->attributes->set('_controller', '...');

$response = $kernel->handle($request, HttpKernelInterface::SUB_REQUEST);
// do something with this response
```

This creates another full request-response cycle where this new ```Request``` is transformed into a ```Response```. **The only difference internally is that some listeners (e.g. security) may only act upon the main request**. Each listener is passed some subclass of KernelEvent, whose **isMainRequest()** method can be used to check if the current request is a "main" or "sub" request.


## Official best practices
- [Symfony Best Practices - symfony.com](https://symfony.com/doc/5.0/best_practices/index.html)

## Release management
- [The Release Process - symfony.com](https://symfony.com/doc/5.0/contributing/community/releases.html)

## Backward compatibility promise
- [Our Backwards Compatibility Promise - symfony.com](https://symfony.com/doc/5.0/contributing/code/bc.html)

## Deprecations best practices
- [Deprecations - symfony.com](https://symfony.com/doc/6.0/contributing/code/conventions.html#deprecations)

A feature is marked as deprecated by adding a @deprecated PHPDoc to relevant classes, methods, properties, ...,  
The deprecation message must indicate the version in which the feature was deprecated, and whenever possible, how it was replaced,  
When the replacement is in another namespace than the deprecated class, its FQCN must be used,  
```
/**
 * @deprecated since Symfony 5.1, use A\B\Replacement instead.
 */
 ```
A deprecation must also be triggered to help people with the migration (requires the symfony/deprecation-contracts package):

```
trigger_deprecation('symfony/package-name', '5.1', 'The "%s" class is deprecated, use "%s" instead.', Deprecated::class, Replacement::class);
```

When deprecating a whole class the trigger_deprecation() call should be placed after the use declarations.


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
- [Method Names - symfony.com](https://symfony.com/doc/6.0/contributing/code/conventions.html#method-names)
- [Conventions - symfony.com](https://symfony.com/doc/6.0/contributing/code/standards.html)

Naming Conventions
- Use camelCase for PHP variables, function and method names, arguments (e.g. $acceptableContentTypes, hasSession());
- Use snake_case for configuration parameters and Twig template variables (e.g. framework.csrf_protection, http_status_code);
- Use SCREAMING_SNAKE_CASE for constants (e.g. InputArgument::IS_ARRAY);
- Use UpperCamelCase for enumeration cases (e.g. InputArgumentMode::IsArray);
- Use namespaces for all PHP classes, interfaces, traits and enums and UpperCamelCase for their names (e.g. ConsoleLogger);
- Prefix all abstract classes with Abstract except PHPUnit \*TestCase. Please note some early Symfony classes do not follow this convention and have not been renamed for backward compatibility reasons. However, all new abstract classes must follow this naming convention;
- Suffix interfaces with Interface;
- Suffix traits with Trait;
- Don't use a dedicated suffix for classes or enumerations (e.g. like Class or Enum), except for the cases listed below.
- Suffix exceptions with Exception;
- Prefix PHP attributes with As where applicable (e.g. #[AsCommand] instead of #[Command], but #[When] is kept as-is);
- Use UpperCamelCase for naming PHP files (e.g. EnvVarProcessor.php) and snake case for naming Twig templates and web assets (section_layout.html.twig, index.scss);
- For type-hinting in PHPDocs and casting, use bool (instead of boolean or Boolean), int (instead of integer), float (instead of double or real);
- Don't forget to look at the more verbose Conventions document for more subjective naming considerations.

Service Naming Conventions
- A service name must be the same as the fully qualified class name (FQCN) of its class (e.g. App\EventSubscriber\UserSubscriber);
- If there are multiple services for the same class, use the FQCN for the main service and use lowercase and underscored names for the rest of services. Optionally divide them in groups separated with dots (e.g. something.service_name, fos_user.something.service_name);
- Use lowercase letters for parameter names (except when referring to environment variables with the %env(VARIABLE_NAME)% syntax);
- Add class aliases for public services (e.g. alias Symfony\Component\Something\ClassName to something.service_name).

