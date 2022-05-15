---
title: Routing - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Routing
- [Routing - symfony.com](https://symfony.com/doc/6.0/routing.html)

## Configuration (YAML, XML, PHP & attributes/annotations)
- [Creating Routes - symfony.com](https://symfony.com/doc/6.0/routing.html#creating-routes)

Routes can be configured in YAML, XML, PHP or using either attributes or annotations. All formats provide the same features and performance, so choose your favorite. Symfony **recommends attributes** because it's convenient to put the route and controller in the same place.

## Parameters

### Parameters Validation :  

The requirements option defines the PHP regular expressions that route parameters must match for the entire route to match. In this example, \d+ is a regular expression that matches a digit of any length.
```
/**
 * @Route("/blog/{page}", name="blog_list", requirements={"page"="\d+"})
 */
 public function list(int $page): Response
    {
 ```    
If you prefer, requirements can be inlined in each parameter using the syntax `{parameter_name<requirements>}`. This feature makes configuration more concise, but it can decrease route readability when requirements are complex:

```
/**
 * @Route("/blog/{page<\d+>}", name="blog_list")
 */
 public function list(int $page): Response
    {
```

### Optional Parameters :

In the previous example, the URL of blog_list is /blog/{page}. If users visit /blog/1, it will match. But if they visit /blog, it will not match. As soon as you add a parameter to a route, **it must have a value**.

You can make blog_list once again match when the user visits /blog by **adding a default value** for the {page} parameter. **When using annotations or attributes, default values are defined in the arguments of the controller action**. **In the other configuration formats** they are defined with the **defaults option**:

```
/**
 * @Route("/blog/{page<\d+>}", name="blog_list")
 */
public function list(int $page = 1): Response
{
```
```
# config/routes.yaml
blog_list:
    path:       /blog/{page}
    controller: App\Controller\BlogController::list
    defaults:
        page: 1
    requirements:
        page: '\d+'

blog_show:
    # ...
```

If you want to **always include some default value in the generated URL** (for example to force the generation of /blog/1 instead of /blog in the previous example) add the ! character before the parameter name: `/blog/{!page}`

As it happens with requirements, default values can also be inlined in each parameter using the syntax `{parameter_name?default_value}`. This feature is compatible with inlined requirements, so you can inline both in a single parameter:
```
 /**
 * @Route("/blog/{page<\d+>?1}", name="blog_list")
 */
public function list(int $page): Response
{
```
### Priority Parameter :

Symfony evaluates routes in the order they are defined. If the path of a route matches many different patterns, it might prevent other routes from being matched. In **YAML and XML** you can move the route definitions **up or down in the configuration file to control their priority**. In routes defined as **PHP annotations or attributes** this is much harder to do, so you can set the optional **priority** parameter in those routes to control their priority
```
/**
 * This route could not be matched without defining a higher priority than 0.
 *
 * @Route("/blog/list", name="blog_list", priority=2)
 */
```
The priority parameter expects an integer value. Routes with higher priority are sorted before routes with lower priority. The default value when it is not defined is 0.

### Parameter Conversion :

To add support for "param converters" we need SensioFrameworkExtraBundle:
```
composer require sensio/framework-extra-bundle
```
```
/**
 * @Route("/blog/{slug}", name="blog_show")
 */
public function show(BlogPost $post): Response
{
```
### Special Parameters :
```
 /**
 * @Route(
 *     "/articles/{_locale}/search.{_format}",
 *     locale="en",
 *     format="html",
 *     requirements={
 *         "_locale": "en|fr",
 *         "_format": "html|xml",
 *     }
 * )
 */
public function search(): Response
```


### Extra Parameters :  

In the defaults option of a route you can optionally define parameters not included in the route configuration. This is useful to pass extra arguments to the controllers of the routes:
```
/**
 * @Route("/blog/{page}", name="blog_index", defaults={"page": 1, "title": "Hello world!"})
 */
public function index(int $page, string $title): Response
{
```

### Slash Characters in Route Parameters : 

Route parameters can contain any values except the / slash character, because that's the character used to separate the different parts of the URLs.
A possible solution is to change the parameter requirements to be more permissive:
```
/**
 * @Route("/share/{token}", name="share", requirements={"token"=".+"})
 */
public function share($token): Response
{
```

## Generate URL parameters
- [Generating URLs - symfony.com](https://symfony.com/doc/6.0/routing.html#generating-urls)

### Generating URLs in Controllers
If your controller extends from the **AbstractController**, use the **generateUrl()** helper:
```
class BlogController extends AbstractController
{
    /**
     * @Route("/blog", name="blog_list")
     */
    public function list(): Response
    {
        // generate a URL with no route arguments
        $signUpPage = $this->generateUrl('sign_up');

        // generate a URL with route arguments
        $userProfilePage = $this->generateUrl('user_profile', [
            'username' => $user->getUserIdentifier(),
        ]);

        // generated URLs are "absolute paths" by default. Pass a third optional
        // argument to generate different URLs (e.g. an "absolute URL")
        $signUpPage = $this->generateUrl('sign_up', [], UrlGeneratorInterface::ABSOLUTE_URL);

        // when a route is localized, Symfony uses by default the current request locale
        // pass a different '_locale' value if you want to set the locale explicitly
        $signUpPageInDutch = $this->generateUrl('sign_up', ['_locale' => 'nl']);

        // ...
    }
```
### Generating URLs in Services
Inject the router Symfony service into your own services and use its **generate()** method. When using service autowiring you only need to add an argument in the service constructor and type-hint it with the **UrlGeneratorInterface** class:
```
// src/Service/SomeService.php
namespace App\Service;

use Symfony\Component\Routing\Generator\UrlGeneratorInterface;

class SomeService
{
    private $router;

    public function __construct(UrlGeneratorInterface $router)
    {
        $this->router = $router;
    }

    public function someMethod()
    {
        // ...

        // generate a URL with no route arguments
        $signUpPage = $this->router->generate('sign_up');

        // generate a URL with route arguments
        $userProfilePage = $this->router->generate('user_profile', [
            'username' => $user->getUserIdentifier(),
        ]);

        // generated URLs are "absolute paths" by default. Pass a third optional
        // argument to generate different URLs (e.g. an "absolute URL")
        $signUpPage = $this->router->generate('sign_up', [], UrlGeneratorInterface::ABSOLUTE_URL);

        // when a route is localized, Symfony uses by default the current request locale
        // pass a different '_locale' value if you want to set the locale explicitly
        $signUpPageInDutch = $this->router->generate('sign_up', ['_locale' => 'nl']);
    }
}
```

### Generating URLs in Commmand

Generating URLs in commands works the same as generating URLs in services. The only difference is that commands are not executed in the HTTP context. Therefore, if you generate absolute URLs, you'll get http://localhost/ as the host name instead of your real host name.

The solution is to configure the default_uri option to define the "request context" used by commands when they generate URLs:

```
# config/packages/routing.yaml
framework:
    router:
        # ...
        default_uri: 'https://example.org/my/path/'
```

## Trigger redirects
- [How to Configure a Redirect without a custom Controller - symfony.com](https://symfony.com/doc/current/routing.html#redirecting-to-urls-and-routes-directly-from-a-route)

Use the **RedirectController** to redirect to other routes and URLs:
```
# config/routes.yaml
doc_shortcut:
    path: /doc
    controller: Symfony\Bundle\FrameworkBundle\Controller\RedirectController
    defaults:
        route: 'doc_page'
        # optionally you can define some arguments passed to the route
        page: 'index'
        version: 'current'
        # redirections are temporary by default (code 302) but you can make them permanent (code 301)
        permanent: true
        # add this to keep the original query string parameters when redirecting
        keepQueryParams: true
        # add this to keep the HTTP method when redirecting. The redirect status changes
        # * for temporary redirects, it uses the 307 status code instead of 302
        # * for permanent redirects, it uses the 308 status code instead of 301
        keepRequestMethod: true

legacy_doc:
    path: /legacy/doc
    controller: Symfony\Bundle\FrameworkBundle\Controller\RedirectController
    defaults:
        # this value can be an absolute path or an absolute URL
        path: 'https://legacy.example.com/doc'
        permanent: true
```

## Special internal routing attributes
- [Special Routing Parameters - symfony.com](https://symfony.com/doc/6.0/routing.html#special-routing-parameters)

## Sub domain routing
- [How to Match a Route Based on the Host - symfony.com](https://symfony.com/doc/current/routing.html#sub-domain-routing)

Routes can configure a host option to require that the HTTP host of the incoming requests matches some specific value. In the following example, both routes match the same path (/) but one of them only responds to a specific host name:

```
/**
 * @Route("/", name="mobile_homepage", host="m.example.com")
 */
public function mobileHomepage(): Response
{
```
   
```
/**
 * @Route(
 *     "/",
 *     name="mobile_homepage",
 *     host="{subdomain}.example.com",
 *     defaults={"subdomain"="m"},
 *     requirements={"subdomain"="m|mobile"}
 * )
 */
public function mobileHomepage(): Response
{
```

## Conditional request matching
- [How to Restrict Route Matching through Conditions - symfony.com](https://symfony.com/doc/current/routing.html#matching-expressions)

Use the condition option if you need some route to match based on some arbitrary matching logic:

```
// src/Controller/DefaultController.php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

class DefaultController extends AbstractController
{
    /**
     * @Route(
     *     "/contact",
     *     name="contact",
     *     condition="context.getMethod() in ['GET', 'HEAD'] and request.headers.get('User-Agent') matches '/firefox/i'"
     * )
     *
     * expressions can also include configuration parameters:
     * condition: "request.headers.get('User-Agent') matches '%app.allowed_browsers%'"
     */
    public function contact(): Response
    {
        // ...
    }
}
```

The value of the condition option is any valid ExpressionLanguage expression and can use any of these variables created by Symfony:

`context` : An instance of RequestContext, which holds the most fundamental information about the route being matched.  
`request` : The Symfony Request object that represents the current request.  
`env(string $name)` : Returns the value of a variable using Environment Variable Processors  

Behind the scenes, expressions are compiled down to raw PHP. Because of this, using the condition key causes no extra overhead beyond the time it takes for the underlying PHP to execute.


## HTTP methods matching
- [Set the Request Parameters - symfony.com](https://symfony.com/doc/6.0/components/routing.html#set-the-request-parameters)
- [Adding HTTP Method Requirements - symfony.com](https://symfony.com/doc/6.0/routing/requirements.html#adding-http-method-requirements)

## User's locale guessing
- [How to Work with the User's Locale - symfony.com](https://symfony.com/doc/6.0/translation/locale.html)

The locale of the current user is stored in the request and is accessible via the **Request object**:

```
use Symfony\Component\HttpFoundation\Request;

public function index(Request $request)
{
    $locale = $request->getLocale();
}
```
To set the user's locale, you may want to create a **custom event listener** so that it's set before any other parts of the system (i.e. the translator) need it:

```
public function onKernelRequest(RequestEvent $event)
{
    $request = $event->getRequest();

    // some logic to determine the $locale
    $request->setLocale($locale);
}
```
**The custom listener must be called before LocaleListener**, which initializes the locale based on the current request. To do so, set your listener priority to a higher value than LocaleListener priority (which you can obtain by running the debug:event kernel.request command).

Setting the locale using $request->setLocale() in the controller is too late to affect the translator. Either set the locale via a **listener (like above)**, **the URL**  or **call setLocale()** directly on the translator service.

### The Local and the URL :

Since you can store the locale of the user in the session, it may be tempting to use the same URL to display a resource in different languages based on the user's locale. For example, http://www.example.com/contact could show content in English for one user and French for another user. Unfortunately, this violates a fundamental rule of the Web: that a particular URL returns the same resource regardless of the user. To further muddy the problem, which version of the content would be indexed by search engines?

A better policy is to include the locale in the URL using the special _locale parameter:

```
# config/routes.yaml
contact:
    path:       /{_locale}/contact
    controller: App\Controller\ContactController::index
    requirements:
        _locale: en|fr|de
```
When using the special `_locale` parameter in a route, the matched locale **is automatically set on the Request** and can be retrieved via the `getLocale()` method. In other words, if a user visits the URI /fr/contact, the locale fr will automatically be set as the locale for the current request.

You can now use the locale to create routes to other translated pages in your application.

### Setting a Default Locale : 
What if the user's locale hasn't been determined? You can guarantee that a locale is set on each user's request by defining a default_locale for the framework:

```
# config/packages/translation.yaml
framework:
    default_locale: en
```

## Router debugging
- [How to Visualize And Debug Routes - symfony.com](https://symfony.com/doc/6.0/routing/debug.html)

`debug:router` : command lists all your application routes in the same order in which Symfony evaluates them  
`router:match` : command shows which route will match the given URL. It's useful to find out why some URL is not executing the controller action that you expect
