---
title: "Authenticator"
subtitle: "Using the HTTP Authenticator"
---

[TOC]

## Creating the Authenticator

The workflow is easy. Just create an authenticator in the first step and secure your resource by checking for credentials with a second step.

I strongly recommend using a library like [PHP dotenv](https://github.com/vlucas/phpdotenv) to store the credentials and keep usernames and passwords out of version control.

### Using the Class Constructor

```php
use Intervention\HttpAuth\Authenticator;

$auth = new Authenticator(
   'basic', // auth type
   'Secure Resource', // name of realm
   'admin', // username
   'secret' // password
);
```

Alternatively use methods to set properties.

```php
use Intervention\HttpAuth\Authenticator;

$auth = new Authenticator();
$auth->withType('digest');
$auth->withRealm('Secure');
$auth->withCredentials('admin', 'secret');
```

### Using Static Factory Methods

The package comes with several static factory methods to create the authenticator.

```php
use Intervention\HttpAuth\Authenticator;

// create basic auth by array
$auth = Authenticator::make([
    'type' => 'basic',
    'realm' => 'Secure Resource',
    'username' => 'admin',
    'password' => 'secret',
]);
```

Or create an authenticator by defining the authentication type directly.

```php
use Intervention\HttpAuth\Authenticator;

// create basic auth instance
$auth = Authenticator::basic('Secured Realm')->withCredentials('admin', 'secret');

// create digest authenticator
$auth = Authenticator::digest('Secured Realm')->withCredentials('admin', 'secret');
```

## Securing the Resource

After you created a HTTP authenticator instance, you have to call `secure()` to secure the resource by checking for credentials. Otherwise nothing will happen.

The server will send a HTTP response with the status code 401 and the browser will ask the user for a username and a password.


```php
use Intervention\HttpAuth\Authenticator;

// creating authenticator and checking credentials
Authenticator::make()->withCredentials('admin', 'secret')->secure();
```

### Customizing Notice

Optionally you can provide a status message, which will be displayed to the user, when the credential check failed.

```php
use Intervention\HttpAuth\Authenticator;

// proving custom message for users with failed credential check
Authenticator::basic()->secure('Sorry, no access.');
```
