---
title: Security - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# Security
- [Security - symfony.com](https://symfony.com/doc/6.0/security.html)

## Authentication
- [Authentication - symfony.com](https://symfony.com/doc/5.0/components/security/authentication.html)
- [How to Build a Traditional Login Form - symfony.com](https://symfony.com/doc/5.0/security/form_login_setup.html)
- [How to Load Security Users from the Database (the Entity Provider) - symfony.com](https://symfony.com/doc/5.0/security/entity_provider.html)
- [How to Impersonate a User - symfony.com](https://symfony.com/doc/5.0/security/impersonating_user.html)
- [How to Authenticate Users with API Keys - symfony.com](https://symfony.com/doc/5.0/security/api_key_authentication.html)

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

## Guard authenticators
- [How to Create a Custom Authentication System with Guard - symfony.com](https://symfony.com/doc/5.0/security/guard_authentication.html)

## Voters and voting strategies
- [How to Use Voters to Check User Permissions - symfony.com](https://symfony.com/doc/5.0/security/voters.html)
