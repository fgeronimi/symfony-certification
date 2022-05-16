---
title: Templating with Twig - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Twig syntax up to 3.3 version
- [Twig for Template Designers - twig.sensiolabs.org](https://twig.symfony.com/doc/3.x/)

The rendering of a Twig template can be summarized into four key steps:

**Load the template**: If the template is already compiled, load it and go to the evaluation step, otherwise:  

First, the **lexer** tokenizes the template source code into small pieces for easier processing;  
Then, the **parser** converts the token stream into a meaningful tree of nodes (the Abstract Syntax Tree);  
Finally, the **compiler** transforms the AST into PHP code.  

**Evaluate the template**: It means calling the display() method of the compiled template and passing it the context.


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
- [Output Escaping - symfony.com](https://symfony.com/doc/6.0/templating.html#output-escaping)

To prevent (XSS) attack, use "output escaping" to transform the characters which have special meaning (e.g. replace < by the &lt; HTML entity). Symfony applications are safe by default because they perform automatic output escaping thanks to the **Twig autoescape** option:

```
<p>Hello {{ name }}</p>
{# if 'name' is '<script>alert('hello!')</script>', Twig will output this:
   '<p>Hello &lt;script&gt;alert(&#39;hello!&#39;)&lt;/script&gt;</p>' #}
```
If you are rendering a variable that is trusted and contains HTML contents, use the **Twig raw** filter to disable the output escaping for that variable:

```
<h1>{{ product.title|raw }}</h1>
{# if 'product.title' is 'Lorem <strong>Ipsum</strong>', Twig will output
   exactly that instead of 'Lorem &lt;strong&gt;Ipsum&lt;/strong&gt;' #}
```

## Template inheritance
- [Template Inheritance and Layouts - symfony.com](https://symfony.com/doc/6.0/templating.html#template-inheritance-and-layouts)
- [How to Organize Your Twig Templates Using Inheritance - symfony.com](https://symfony.com/doc/5.0/templating/inheritance.html)

**Parent block :**
```
{% block sidebar %}
    <h3>Table Of Contents</h3>
    ...
    {{ parent() }}
{% endblock %}
```
**Named Block End-Tags :**
```
{% block sidebar %}
    {% block inner_sidebar %}
        ...
    {% endblock inner_sidebar %}
{% endblock sidebar %}
```
**Block Nesting and Scope** (Blocks can be nested for more complex layouts. Per default, blocks have access to variables from outer scopes) :
```
{% for item in seq %}
    <li>{% block loop_item %}{{ item }}{% endblock %}</li>
{% endfor %}
```
**Block Shortcuts** (For blocks with little content, it's possible to use a shortcut syntax. The following constructs do the same thing) :
```
{% block title %}
    {{ page_title|title }}
{% endblock %}
{% block title page_title|title %}
```
**Dynamic Inheritance** (You can also provide a list of templates that are checked for existence. The first template that exists will be used as a parent) :
```
{% extends ['layout.html', 'base_layout.html'] %}
```
**Conditional Inheritance : **
```
{% extends standalone ? "minimum.html" : "base.html" %}
```

When rendering a template, Symfony looks for it first in the twig.paths directories that don't define a namespace and then falls back to the default template directory (usually, templates/).
```
# config/packages/twig.yaml
twig:
    # ...
    paths:
        # directories are relative to the project root dir (but you
        # can also use absolute directories)
        'email/default/templates': ~
        'backend/templates': ~
```



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
`app.session` : The Session object that represents the current user's session or null if there is none.  
`app.flashes` : An array of all the flash messages stored in the session. You can also get only the messages of some type (e.g. app.flashes('notice')).  
`app.environment` : The name of the current configuration environment (dev, prod, etc).  
`app.debug` : True if in debug mode. False otherwise.  
`app.token` : A TokenInterface object representing the security token.  

In addition to the global app variable injected by Symfony, you can also inject variables automatically to all Twig templates.

- [How to Inject Variables into all Templates (i.e. global Variables - symfony.com](https://symfony.com/doc/5.0/templating/global_variables.html)

## Filters and functions
- [Filters - twig.symfony.com](https://twig.symfony.com/doc/3.x/filters/index.html)
- [Functions - twig.symfony.com](https://twig.symfony.com/doc/3.x/functions/index.html)

## Template includes
- [Including other templates - symfony.com](https://symfony.com/doc/6.0/templating.html#including-other-templates)

The **include() Twig** function takes as argument the path of the template to include. The included template has access to all the variables of the template that includes it (use the with_context option to control this).

You can also pass variables to the included template. This is useful for example to rename variables. Imagine that your template stores the user information in a variable called blog_post.author instead of the user variable that the template fragment expects. Use the following to rename the variable:

```
{# templates/blog/index.html.twig #}

{# ... #}
{{ include('blog/_user_profile.html.twig', {user: blog_post.author}) }}
```

## Loops and conditions
- [For - twig.symfony.com](https://twig.symfony.com/doc/3.x/tags/for.html)

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
- [How to Embed Controllers in a Template - symfony.com](https://symfony.com/doc/6.0/templating/embedding_controllers.html)

Including template fragments is useful to reuse the same content on several pages. However, this technique is not the best solution in some cases.

Imagine that the template fragment displays the three most recent blog articles. To do that, it needs to make a database query to get those articles. **When using the include() function**, you'd need to do the same database query in every page that includes the fragment. This is not very convenient.

A better alternative is to embed the result of executing some controller with the **render() and controller() Twig functions**.
```
{# templates/base.html.twig #}

{# ... #}
<div id="sidebar">
    {# if the controller is associated with a route, use the path() or url() functions #}
    {{ render(path('latest_articles', {max: 3})) }}
    {{ render(url('latest_articles', {max: 3})) }}

    {# if you don't want to expose the controller with a public URL,
       use the controller() function to define the controller to execute #}
    {{ render(controller(
        'App\\Controller\\BlogController::recentArticles', {max: 3}
    )) }}
</div>
```

## Translations and pluralization
- [Translations - symfony.com](https://symfony.com/doc/6.0/translation.html)

### Using Twig Tags
Symfony provides a specialized Twig tag trans to help with message translation of static blocks of text:
```
{% trans %}Hello %name%{% endtrans %}
```
The %var% notation of placeholders is required when translating in Twig templates using the tag.
If you need to use the percent character (%) in a string, escape it by doubling it: {% trans %}Percent: %percent%%%{% endtrans %}

You can also specify the message domain and pass some additional variables:

```
{% trans with {'%name%': 'Fabien'} from 'app' %}Hello %name%{% endtrans %}

{% trans with {'%name%': 'Fabien'} from 'app' into 'fr' %}Hello %name%{% endtrans %}
```
### Using Twig Filters
The trans filter can be used to translate variable texts and complex expressions:

```
{{ message|trans }}
{{ message|trans({'%name%': 'Fabien'}, 'app') }}
```
Using the **translation tags or filters have the same effect**, but with one subtle difference: **automatic output escaping is only applied to translations using a filter**. In other words, if you need to be sure that your translated message is not output escaped, you must apply the raw filter after the translation filter:
```
{# text translated between tags is never escaped #}
{% trans %}
    <h3>foo</h3>
{% endtrans %}

{% set message = '<h3>foo</h3>' %}

{# strings and variables translated via a filter are escaped by default #}
{{ message|trans|raw }}
{{ '<h3>bar</h3>'|trans|raw }}
You can set the translation domain for an entire Twig template with a single tag:
```

```
{% trans_default_domain 'app' %}
```
Note that this **only influences the current template, not any "included" template** (in order to avoid side effects).

## String interpolation
- [Twig's string interpolation feature - twig.symfony.com](https://twig.symfony.com/doc/3.x/templates.html#string-interpolation)

String interpolation (#{expression}) allows any valid expression to appear within a double-quoted string. The result of evaluating that expression is inserted into the string:
```
{{ "foo #{bar} baz" }}
{{ "foo #{1 + 2} baz" }}
```

## Assets management
- [Managing CSS and Javascript - symfony.com](https://symfony.com/doc/6.0/frontend.html)

## Debugging variables
- [How to Dump Debug Information in Twig Templates](https://symfony.com/doc/6.0/templating/debug.html)

Then, use either the **{% dump %}** tag or the **{{ dump() }}** function depending on your needs:

```
{# templates/article/recent_list.html.twig #}
{# the contents of this variable are sent to the Web Debug Toolbar
   instead of dumping them inside the page contents #}
{% dump articles %}

{% for article in articles %}
    {# the contents of this variable are dumped inside the page contents
       and they are visible on the web page #}
    {{ dump(article) }}

    <a href="/article/{{ article.slug }}">
        {{ article.title }}
    </a>
{% endfor %}
```


