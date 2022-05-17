---
title: HTTP Caching - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# HTTP Caching
- [HTTP Cache - symfony.com](https://symfony.com/doc/6.0/http_cache.html)
- [Things Caches Do - tomayko.com](https://tomayko.com/blog/2008/things-caches-do)
- [Caching Tutorial - mnot.net](https://www.mnot.net/cache_docs/)
- [HTTP caching - developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
- [HTTP Caching Web Fundamentals - developers.google.com](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching)

## Cache types (browser, proxies, and reverse-proxies)
- [Kinds of Web Caches - Caching Tutorial - mnot.net](https://www.mnot.net/cache_docs/#KINDS)

## Expiration (Expires, Cache-Control)
- [HTTP Cache Expiration - symfony.com](https://symfony.com/doc/5.0/http_cache/expiration.html)
- [Expiration - Things Caches Do - tomayko.com](https://tomayko.com/blog/2008/things-caches-do#expiration)

Expiration Caching Used to cache your entire response for a specific amount of time (e.g. 24 hours). Simple, but cache invalidation is more difficult.
The expiration model can be accomplished using one of two, nearly identical, HTTP headers: **Expires** or **Cache-Control**.


**Expiration with the Cache-Control Header :** 
```
// src/Controller/BlogController.php
use Symfony\Component\HttpFoundation\Response;
// ...

public function index()
{
    // somehow create a Response object, like by rendering a template
    $response = $this->render('blog/index.html.twig', []);

    // cache publicly for 3600 seconds
    $response->setPublic();
    $response->setMaxAge(3600);

    // (optional) set a custom Cache-Control directive
    $response->headers->addCacheControlDirective('must-revalidate', true);

    return $response;
}
```

**Expiration with the Expires Header :**
```
$date = new DateTime();
$date->modify('+600 seconds');

$response->setExpires($date);
```


## Validation (ETag, Last-Modified)
- [HTTP Cache Validation - symfony.com](https://symfony.com/doc/5.0/http_cache/validation.html)
- [Validation - Things Caches Do - tomayko.com](https://tomayko.com/blog/2008/things-caches-do#validation)

Validation Caching More complex: used to cache your response, but allows you to dynamically invalidate it as soon as your content changes.
Like with expiration, there are two different HTTP headers that can be used to implement the validation model: **ETag** and **Last-Modified**.

**Validation with the ETag Header :**
```
// src/Controller/DefaultController.php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Request;

class DefaultController extends AbstractController
{
    public function homepage(Request $request)
    {
        $response = $this->render('static/homepage.html.twig');
        $response->setEtag(md5($response->getContent()));
        $response->setPublic(); // make sure the response is public/cacheable
        $response->isNotModified($request);

        return $response;
    }
}
```
The **isNotModified()** method compares the If-None-Match header with the ETag response header. If the two match, the method automatically sets the Response status code to 304.

**Validation with the Last-Modified Header :**
```
// src/Controller/ArticleController.php
namespace App\Controller;

// ...
use App\Entity\Article;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

class ArticleController extends AbstractController
{
    public function show(Article $article, Request $request)
    {
        $author = $article->getAuthor();

        $articleDate = new \DateTime($article->getUpdatedAt());
        $authorDate = new \DateTime($author->getUpdatedAt());

        $date = $authorDate > $articleDate ? $authorDate : $articleDate;

        $response = new Response();
        $response->setLastModified($date);
        // Set response as public. Otherwise it will be private by default.
        $response->setPublic();

        if ($response->isNotModified($request)) {
            return $response;
        }

        // ... do more work to populate the response with the full content

        return $response;
    }
}
```
The **isNotModified()** method compares the If-Modified-Since header with the Last-Modified response header. If they are equivalent, the Response will be set to a 304 status code.

## Client side caching
- [Browser Caches - Caching Tutorial - mnot.net](https://www.mnot.net/cache_docs/#BROWSER)
- [Private browser caches - HTTP caching - developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#Private_browser_caches)

## Server side caching
- [Caching with a Gateway Cache - symfony.com](https://symfony.com/doc/5.0/http_cache.html#caching-with-a-gateway-cache)
- [Gateway Caches - Caching Tutorial - mnot.net](https://www.mnot.net/cache_docs/#GATEWAY)

## Edge Side Includes
- [Working with Edge Side Includes - symfony.com](https://symfony.com/doc/5.0/http_cache/esi.html)
- [Caching Pages that Contain CSRF Protected Forms - symfony.com](https://symfony.com/doc/5.0/http_cache/form_csrf_caching.html)
