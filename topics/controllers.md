---
title: Controllers - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Controllers
- [Controller - symfony.com](https://symfony.com/doc/6.0/controller.html)

## Naming conventions
- [Controller Naming Pattern - symfony.com](https://symfony.com/doc/5.0/routing.html#controller-naming-pattern)

## The base AbstractController class
- [AbstractController.php - github.com](https://github.com/symfony/symfony/blob/5.0/src/Symfony/Bundle/FrameworkBundle/Controller/AbstractController.php)

## The request
- [The Request and Response Object - symfony.com](https://symfony.com/doc/5.0/controller.html#the-request-and-response-object)
- [Request.php - github.com](https://github.com/symfony/http-foundation/blob/5.0/Request.php)

## The response
- [Response.php - github.com](https://github.com/symfony/http-foundation/blob/5.0/Response.php)

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
