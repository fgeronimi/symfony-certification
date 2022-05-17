---
title: Security - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Security
- [Security - symfony.com](https://symfony.com/doc/6.0/security.html)

## Authentication
- [Authentication - symfony.com](https://symfony.com/doc/6.0/components/security/authentication.html)
- [How to Build a Traditional Login Form - symfony.com](https://symfony.com/doc/5.0/security/form_login_setup.html)
- [How to Load Security Users from the Database (the Entity Provider) - symfony.com](https://symfony.com/doc/5.0/security/entity_provider.html)
- [How to Impersonate a User - symfony.com](https://symfony.com/doc/5.0/security/impersonating_user.html)
- [How to Authenticate Users with API Keys - symfony.com](https://symfony.com/doc/5.0/security/api_key_authentication.html)

During authentication, the system tries to find a matching user for the visitor of the webpage. Traditionally, this was done using a login form or a HTTP basic dialog in the browser. However, the SecurityBundle comes with many other authenticators:
- Form Login
- JSON Login
- HTTP Basic
- Login Link
- X.509 Client Certificates
- Remote users
- Custom Authenticators


### Authentication Events

![http_kernel](https://symfony.com/doc/current/_images/security/security_events.svg)

- **CheckPassportEvent** : Dispatched after the authenticator created the security passport. Listeners of this event do the actual authentication checks (like checking the passport, validating the CSRF token, etc.)
- **AuthenticationTokenCreatedEvent** : Dispatched after the passport was validated and the authenticator created the security token (and user). This can be used in advanced use-cases where you need to modify the created token (e.g. for multi factor authentication).
- **AuthenticationSuccessEvent** : Dispatched when authentication is nearing success. This is the last event that can make an authentication fail by throwing an AuthenticationException.
- **LoginSuccessEvent** : Dispatched after authentication was fully successful. Listeners to this event can modify the response sent back to the user.
- **LoginFailureEvent** : Dispatched after an AuthenticationException was thrown during authentication. Listeners to this event can modify the error response sent back to the user.

### Other Events

- **LogoutEvent** : Dispatched just before a user logs out of your application. See Security.
- **TokenDeauthenticatedEvent** : Dispatched when a user is deauthenticated, for instance because the password was changed. See Security.
- **SwitchUserEvent** : Dispatched after impersonation is completed. See How to Impersonate a User.


## Authorization
- [Denying Access, Roles and other Authorization - symfony.com](https://symfony.com/doc/5.0/security.html#denying-access-roles-and-other-authorization)

## Configuration
- [Initial security.yml Setup (Authentication) - symfony.com](https://symfony.com/doc/5.0/security.html#initial-security-yml-setup-authentication)

## Providers
- [How to Create a custom Authentication Provider - symfony.com](https://symfony.com/doc/5.0/security/custom_authentication_provider.html)
- [How to Create a custom User Provider - symfony.com](https://symfony.com/doc/5.0/security/custom_provider.html)

## Firewalls
- [Firewalls - symfony.com](https://symfony.com/doc/6.0/security.html#the-firewall)

The firewalls section of config/packages/security.yaml is the most important section. A "firewall" is your authentication system: the firewall defines which parts of your application are secured and how your users will be able to authenticate (e.g. login form, API token, etc).

- [How to Restrict Firewalls to a Specific Request - symfony.com](https://symfony.com/doc/6.0/security/firewall_restriction.html)

```
# config/packages/security.yaml

# ...
security:
    firewalls:
        secured_area:
            pattern: ^/admin // Restricting by Path
            host: ^admin\.example\.com$ // Restricting by Host
            methods: [GET, POST] // Restricting by HTTP Methods
            # ...
```





## Users
- [The Users - symfony.com](https://symfony.com/doc/current/security.html#the-user)

Permissions in Symfony are always linked to a user object. If you need to secure (parts of) your application, you need to create a user class. This is a class that implements **UserInterface.** This is often a Doctrine entity, but you can also use a dedicated Security user class.

User providers are used in a couple places during the security lifecycle:

- **Load the User based on an identifier** : During login (or any other authenticator), the provider loads the user based on the user identifier. Some other features, like user impersonation and Remember Me also use this.
- **Reload the User from the session** : At the beginning of each request, the user is loaded from the session (unless your firewall is stateless). The provider "refreshes" the user (e.g. the database is queried again for fresh data) to make sure all user information is up to date (and if necessary, the user is de-authenticated/logged out if something changed). See Security for more information about this process.

Symfony comes with several built-in user providers:

- Entity User Provider : Loads users from a database using Doctrine;
- LDAP User Provider : Loads users from a LDAP server;
- Memory User Provider : Loads users from a configuration file;
- Chain User Provider : Merges two or more user providers into a new user provider.

The built-in user providers cover the most common needs for applications, but you can also create your own custom user provider.

Many applications require a user to log in with a password. For these applications, the **SecurityBundle provides password hashing and verification functionality.**
MMake sure your User class implements the **PasswordAuthenticatedUserInterface** and make sure you configure which password hasher should be used for this class in your security.yaml :

```
# config/packages/security.yaml
security:
    # ...
    password_hashers:
        # Use native password hasher, which auto-selects and migrates the best
        # possible hashing algorithm (which currently is "bcrypt")
        Symfony\Component\Security\Core\User\PasswordAuthenticatedUserInterface: 'auto'
```

## Passwords encoders
- [Encoding the User's Password - symfony.com](https://symfony.com/doc/5.0/security.html#c-encoding-the-user-s-password)
- [How to Manually Encode a Password - symfony.com](https://symfony.com/doc/5.0/security/password_encoding.html)

## Roles
- [Roles - symfony.com](https://symfony.com/doc/5.0/security.html#roles)

## Access Control Rules

There are two ways to deny access to something:

- access_control in security.yaml allows you to protect URL patterns (e.g. `/admin/*`). Simpler, but less flexible;
- in your controller (or other code).

```
# config/packages/security.yaml
security:
    # ...

    firewalls:
        # ...
        main:
            # ...

    access_control:
        # require ROLE_ADMIN for /admin*
        - { path: '^/admin', roles: ROLE_ADMIN }

        # or require ROLE_ADMIN or IS_AUTHENTICATED_FULLY for /admin*
        - { path: '^/admin', roles: [IS_AUTHENTICATED_FULLY, ROLE_ADMIN] }

        # the 'path' value can be any valid regular expression
        # (this one will match URLs like /api/post/7298 and /api/comment/528491)
        - { path: ^/api/(post|comment)/\d+$, roles: ROLE_USER }
```
```
// src/Controller/AdminController.php
// ...

public function adminDashboard(): Response
{
    $this->denyAccessUnlessGranted('ROLE_ADMIN');

    // or add an optional message - seen by developers
    $this->denyAccessUnlessGranted('ROLE_ADMIN', null, 'User tried to access a page without having ROLE_ADMIN');
}
```

```
// src/Controller/AdminController.php
// ...

use Sensio\Bundle\FrameworkExtraBundle\Configuration\IsGranted;

/**
 * Require ROLE_ADMIN for all the actions of this controller
 *
 * @IsGranted("ROLE_ADMIN")
 */
class AdminController extends AbstractController
{
    /**
     * Require ROLE_SUPER_ADMIN only for this action
     *
     * @IsGranted("ROLE_SUPER_ADMIN")
     */
    public function adminDashboard(): Response
    {
        // ...
    }
}
```
```
{% if is_granted('ROLE_ADMIN') %}
    <a href="...">Delete</a>
{% endif %}
```
```
if ($this->security->isGranted('ROLE_SALES_ADMIN')) {
     $salesData['top_secret_numbers'] = rand();
}
```
### Allowing Unsecured Access (i.e. Anonymous Users) :

In the access_control configuration, you can use the **PUBLIC_ACCESS** security attribute to exclude some routes for unauthenticated access (e.g. the login page):

```
# config/packages/security.yaml
security:

    # ...
    access_control:
        # allow unauthenticated users to access the login form
        - { path: ^/admin/login, roles: PUBLIC_ACCESS }

        # but require authentication for all other admin routes
        - { path: ^/admin, roles: ROLE_ADMIN }
```

### Checking to see if a User is Logged In (IS_AUTHENTICATED_FULLY)


IS_AUTHENTICATED_FULLY isn't a role, but it kind of acts like one, and every user that has logged in will have this. Actually, there are some special attributes like this:

- **IS_AUTHENTICATED_REMEMBERED**: All logged in users have this, even if they are logged in because of a "remember me cookie". Even if you don't use the remember me functionality, you can use this to check if the user is logged in.
- **IS_AUTHENTICATED_FULLY**: This is similar to IS_AUTHENTICATED_REMEMBERED, but stronger. Users who are logged in only because of a "remember me cookie" will have  IS_AUTHENTICATED_REMEMBERED but will not have IS_AUTHENTICATED_FULLY.
- **IS_REMEMBERED**: Only users authenticated using the remember me functionality, (i.e. a remember-me cookie).
- **IS_IMPERSONATOR**: When the current user is impersonating another user in this session, this attribute will match.

## Guard authenticators
- [How to Create a Custom Authentication System with Guard - symfony.com](https://symfony.com/doc/5.0/security/guard_authentication.html)

## Voters and voting strategies
- [How to Use Voters to Check User Permissions - symfony.com](https://symfony.com/doc/5.0/security/voters.html)
