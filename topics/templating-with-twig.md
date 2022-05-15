---
title: Templating with Twig - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Twig syntax up to 3.3 version
- [Twig for Template Designers - twig.sensiolabs.org](https://twig.symfony.com/doc/3.x/)

# Templating with Twig
- [Creating and Using Templates - symfony.com](https://symfony.com/doc/6.0/templating.html)
- [Twig for Template Designers - twig.sensiolabs.org](https://twig.sensiolabs.org/doc/3.x/templates.html)

### Template Variables
When using the foo.bar notation, Twig tries to get the value of the variable in the following order:

`$foo['bar']` (array and element);  
`$foo->bar` (object and public property);  
`$foo->bar()` (object and public method);  
`$foo->getBar()` (object and getter method);  
`$foo->isBar()` (object and isser method);  
`$foo->hasBar()` (object and hasser method);  

If none of the above exists, use null (or throw a Twig\Error\RuntimeError exception if the strict_variables option is enabled).

This allows to evolve your application code without having to change the template code (you can start with array variables for the application proof of concept, then move to objects with methods, etc.)

### Linking to CSS, JavaScript and Image Assets
If a template needs to link to a static asset (e.g. an image), Symfony provides an asset() Twig function to help generate that URL. First, install the asset package:

`composer require symfony/asset`

You can now use the **asset() function**:

```
{# the image lives at "public/images/logo.png" #}
<img src="{{ asset('images/logo.png') }}" alt="Symfony!"/>

{# the CSS file lives at "public/css/blog.css" #}
<link href="{{ asset('css/blog.css') }}" rel="stylesheet"/>
```
If you need absolute URLs for assets, use the **absolute_url() Twig function** as follows:

```
<img src="{{ absolute_url(asset('images/logo.png')) }}" alt="Symfony!"/>

<link rel="shortcut icon" href="{{ absolute_url('favicon.png') }}">
```

## Auto escaping
- [Output Escaping - symfony.com](https://symfony.com/doc/5.0/templating.html#output-escaping)

## Template inheritance
- [Template Inheritance and Layouts - symfony.com](https://symfony.com/doc/5.0/templating.html#template-inheritance-and-layouts)
- [How to Organize Your Twig Templates Using Inheritance - symfony.com](https://symfony.com/doc/5.0/templating/inheritance.html)

## Global variables
- [How to Access the User, Request, Session & more in Twig via the app Variable - symfony.com](https://symfony.com/doc/6.0/templates.html#the-app-global-variable)

The App Global Variable
Symfony creates a context object that is injected into every Twig template automatically as a variable called app. It provides access to some application information:

```
<p>Username: {{ app.user.username ?? 'Anonymous user' }}</p>
{% if app.debug %}
    <p>Request method: {{ app.request.method }}</p>
    <p>Application Environment: {{ app.environment }}</p>
{% endif %}
```

The `app` variable (which is an instance of AppVariable) gives you access to these variables:

`app.user` : The current user object or null if the user is not authenticated.  
`app.request` : The Request object that stores the current request data (depending on your application, this can be a sub-request or a regular request).  
app.session` : The Session object that represents the current user's session or null if there is none.  
`app.flashes` : An array of all the flash messages stored in the session. You can also get only the messages of some type (e.g. app.flashes('notice')).  
`app.environment` : The name of the current configuration environment (dev, prod, etc).  
`app.debug` : True if in debug mode. False otherwise.  
`app.token` : A TokenInterface object representing the security token.  

In addition to the global app variable injected by Symfony, you can also inject variables automatically to all Twig templates.

- [How to Inject Variables into all Templates (i.e. global Variables - symfony.com](https://symfony.com/doc/5.0/templating/global_variables.html)

## Filters and functions
- [Filters - twig.symfony.com](https://twig.symfony.com/doc/2.x/filters/index.html)
- [Functions - twig.symfony.com](https://twig.symfony.com/doc/2.x/functions/index.html)

## Template includes
- [Including other templates - symfony.com](https://symfony.com/doc/5.0/templating.html#including-other-templates)

## Loops and conditions
- [For - twig.symfony.com](https://twig.symfony.com/doc/2.x/tags/for.html)

## URLs generation
- [Linking to Pages - symfony.com](https://symfony.com/doc/6.0/templates.html#linking-to-pages)

Use the path() Twig function to link to these pages and pass the route name as the first argument and the route parameters as the optional second argument:

```
<a href="{{ path('blog_index') }}">Homepage</a>

{# ... #}

{% for post in blog_posts %}
    <h1>
        <a href="{{ path('blog_post', {slug: post.slug}) }}">{{ post.title }}</a>
    </h1>

    <p>{{ post.excerpt }}</p>
{% endfor %}
```

The **path() function generates relative URLs**. If you need to **generate absolute URLs (for example when rendering templates for emails or RSS feeds), use **the url() function**  which takes the same arguments as path() (e.g. `<a href="{{ url('blog_index') }}"> ... </a>`).


## Controller rendering
- [How to Embed Controllers in a Template - symfony.com](https://symfony.com/doc/5.0/templating/embedding_controllers.html)

## Translations and pluralization
- [Translations - symfony.com](https://symfony.com/doc/5.0/translation.html)

## String interpolation
- [Twig's string interpolation feature - twig.symfony.com](https://twig.symfony.com/doc/1.x/templates.html#string-interpolation)

## Assets management
- [Managing CSS and Javascript - symfony.com](https://symfony.com/doc/6.0/frontend.html)

## Debugging variables
- [How to Dump Debug Information in Twig Templates](https://symfony.com/doc/5.0/templating/debug.html)
