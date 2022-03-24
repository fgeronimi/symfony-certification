---
title: Controllers - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Controllers
- [Controller - symfony.com](https://symfony.com/doc/6.0/controller.html)

## Naming conventions
- [Controller Naming Pattern - symfony.com](https://symfony.com/doc/5.0/routing.html#controller-naming-pattern)

## The base AbstractController class
- [AbstractController.php - github.com](https://github.com/symfony/symfony/blob/6.0/src/Symfony/Bundle/FrameworkBundle/Controller/AbstractController.php)

## The request
- [The Request and Response Object - symfony.com](https://symfony.com/doc/6.0/controller.html#the-request-and-response-object)
- [Request.php - github.com](https://github.com/symfony/http-foundation/blob/6.0/Request.php)

Symfony will pass the Request object to any controller argument that is type-hinted with the Request class:

```
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

public function index(Request $request): Response
{
    $request->isXmlHttpRequest(); // is it an Ajax request?

    $request->getPreferredLanguage(['en', 'fr']);

    // retrieves GET and POST variables respectively
    $request->query->get('page');
    $request->request->get('page');

    // retrieves SERVER variables
    $request->server->get('HTTP_HOST');

    // retrieves an instance of UploadedFile identified by foo
    $request->files->get('foo');

    // retrieves a COOKIE value
    $request->cookies->get('PHPSESSID');

    // retrieves an HTTP request header, with normalized, lowercase keys
    $request->headers->get('host');
    $request->headers->get('content-type');
}
```

The Request class has several public properties and methods that return any information you need about the request.

Like the Request, the Response object has a public headers property. This object is of the type **ResponseHeaderBag** and provides methods for getting and setting response headers. The header names are normalized. As a result, the name Content-Type is equivalent to the name content-type or content_type.



## The response
- [Response.php - github.com](https://github.com/symfony/http-foundation/blob/6.0/Response.php)

**Status codes :** 


- HTTP_CONTINUE = 100;
- HTTP_SWITCHING_PROTOCOLS = 101;
- HTTP_PROCESSING = 102;            // RFC2518
- HTTP_EARLY_HINTS = 103;           // RFC8297
- HTTP_OK = 200;
- HTTP_CREATED = 201;
- HTTP_ACCEPTED = 202;
- HTTP_NON_AUTHORITATIVE_INFORMATION = 203;
- HTTP_NO_CONTENT = 204;
- HTTP_RESET_CONTENT = 205;
- HTTP_PARTIAL_CONTENT = 206;
- HTTP_MULTI_STATUS = 207;          // RFC4918
- HTTP_ALREADY_REPORTED = 208;      // RFC5842
- HTTP_IM_USED = 226;               // RFC3229
- HTTP_MULTIPLE_CHOICES = 300;
- HTTP_MOVED_PERMANENTLY = 301;
- HTTP_FOUND = 302;
- HTTP_SEE_OTHER = 303;
- HTTP_NOT_MODIFIED = 304;
- HTTP_USE_PROXY = 305;
- HTTP_RESERVED = 306;
- HTTP_TEMPORARY_REDIRECT = 307;
- HTTP_PERMANENTLY_REDIRECT = 308;  // RFC7238
- HTTP_BAD_REQUEST = 400;
- HTTP_UNAUTHORIZED = 401;
- HTTP_PAYMENT_REQUIRED = 402;
- HTTP_FORBIDDEN = 403;
- HTTP_NOT_FOUND = 404;
- HTTP_METHOD_NOT_ALLOWED = 405;
- HTTP_NOT_ACCEPTABLE = 406;
- HTTP_PROXY_AUTHENTICATION_REQUIRED = 407;
- HTTP_REQUEST_TIMEOUT = 408;
- HTTP_CONFLICT = 409;
- HTTP_GONE = 410;
- HTTP_LENGTH_REQUIRED = 411;
- HTTP_PRECONDITION_FAILED = 412;
- HTTP_REQUEST_ENTITY_TOO_LARGE = 413;
- HTTP_REQUEST_URI_TOO_LONG = 414;
- HTTP_UNSUPPORTED_MEDIA_TYPE = 415;
- HTTP_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
- HTTP_EXPECTATION_FAILED = 417;
- HTTP_I_AM_A_TEAPOT = 418;                                               // RFC2324
- HTTP_MISDIRECTED_REQUEST = 421;                                         // RFC7540
- HTTP_UNPROCESSABLE_ENTITY = 422;                                        // RFC4918
- HTTP_LOCKED = 423;                                                      // RFC4918
- HTTP_FAILED_DEPENDENCY = 424;                                           // RFC4918
- HTTP_TOO_EARLY = 425;                                                   // RFC-ietf-httpbis-replay-04
- HTTP_UPGRADE_REQUIRED = 426;                                            // RFC2817
- HTTP_PRECONDITION_REQUIRED = 428;                                       // RFC6585
- HTTP_TOO_MANY_REQUESTS = 429;                                           // RFC6585
- HTTP_REQUEST_HEADER_FIELDS_TOO_LARGE = 431;                             // RFC6585
- HTTP_UNAVAILABLE_FOR_LEGAL_REASONS = 451;
- HTTP_INTERNAL_SERVER_ERROR = 500;
- HTTP_NOT_IMPLEMENTED = 501;
- HTTP_BAD_GATEWAY = 502;
- HTTP_SERVICE_UNAVAILABLE = 503;
- HTTP_GATEWAY_TIMEOUT = 504;
- HTTP_VERSION_NOT_SUPPORTED = 505;
- HTTP_VARIANT_ALSO_NEGOTIATES_EXPERIMENTAL = 506;                        // RFC2295
- HTTP_INSUFFICIENT_STORAGE = 507;                                        // RFC4918
- HTTP_LOOP_DETECTED = 508;                                               // RFC5842
- HTTP_NOT_EXTENDED = 510;                                                // RFC2774
- HTTP_NETWORK_AUTHENTICATION_REQUIRED = 511;                             // RFC6585

**HTTP Cache Control directives :** 

```
/**
 * @see https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control
 */
private const HTTP_RESPONSE_CACHE_CONTROL_DIRECTIVES = [
    'must_revalidate' => false,
    'no_cache' => false,
    'no_store' => false,
    'no_transform' => false,
    'public' => false,
    'private' => false,
    'proxy_revalidate' => false,
    'max_age' => true,
    's_maxage' => true,
    'immutable' => false,
    'last_modified' => true,
    'etag' => true,
];
```

## The cookies
- [The HttpFoundation Component - symfony.com](https://symfony.com/doc/5.0/components/http_foundation.html)

## The session
- [Managing the Session - symfony.com](https://symfony.com/doc/5.0/controller.html#managing-the-session)

## The flash messages
- [Flash Messages - symfony.com](https://symfony.com/doc/6.0/controller.html#flash-messages)
```
$this->addFlash(
            'notice',
            'Your changes were saved!'
        );
// $this->addFlash() is equivalent to $request->getSession()->getFlashBag()->add()
```

In the template of the next page (or even better, in your base layout template), read any flash messages from the session using the **flashes()** method provided by the **Twig global app variable**:

```
{# templates/base.html.twig #}

{# read and display just one flash message type #}
{% for message in app.flashes('notice') %}
    <div class="flash-notice">
        {{ message }}
    </div>
{% endfor %}

{# read and display several types of flash messages #}
{% for label, messages in app.flashes(['success', 'warning']) %}
    {% for message in messages %}
        <div class="flash-{{ label }}">
            {{ message }}
        </div>
    {% endfor %}
{% endfor %}

{# read and display all flash messages #}
{% for label, messages in app.flashes %}
    {% for message in messages %}
        <div class="flash-{{ label }}">
            {{ message }}
        </div>
    {% endfor %}
{% endfor %}
```
It's common to use **notice**, **warning** and **error** as the keys of the different types of flash messages, but you can use any key that fits your needs.

You can use the **peek()** method instead to retrieve the message while keeping it in the bag.


## HTTP redirects
- [Redirecting - symfony.com](https://symfony.com/doc/6.0/controller.html#redirecting)  

If you want to redirect the user to another page, use the **redirectToRoute()** and **redirect()**

## Internal redirects
- [How to Forward Requests to another Controller - symfony.com](https://symfony.com/doc/6.0/controller/forwarding.html)  

Though not very common, you can also forward to another controller internally with the **forward()** method provided by the **AbstractController class**.

## Generate 404 pages
- [Managing Errors and 404 Pages - symfony.com](https://symfony.com/doc/5.0/controller.html#managing-errors-and-404-pages)
- [How to Customize Error Pages - symfony.com](https://symfony.com/doc/5.0/controller/error_pages.html)

## File upload
- [How to Upload Files - symfony.com](https://symfony.com/doc/5.0/controller/upload_file.html)

## Built-in internal controllers
- [How to Render a Template directly from a route - symfony.com](https://symfony.com/doc/5.0/templates.html#rendering-a-template-directly-from-a-route)
- [How to Redirect to Urls and Routes directly from a route - symfony.com](https://symfony.com/doc/5.0/routing.html#redirecting-to-urls-and-routes-directly-from-a-route)
