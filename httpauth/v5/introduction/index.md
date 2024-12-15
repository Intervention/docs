# Intervention HttpAuth
## HTTP Authentication Management
Intervention HttpAuth is a PHP library for authenticating resources using HTTP Basic or Digest authentication. Learn how to install and configure the package correctly.

## Introduction

The package [can be easily installed](/v5/introduction/installation) and
provides an API that makes these steps as simple as possible.

The workflow is divided into two steps. In the first, an instance of the
`Authenticator::class` class is created descided which type of authentication
should be used. In the second step, the respective resource is secured by a
single call.

### 1. Create Authenticator Instance

To create authenticator instances you can choose between basic & digest auth.
Simply use the static helper methods described below or [learn how to
instantiate](/v5/api/authenticator) the authenticator in other ways.

#### Create Authenticator Using HTTP Basic Auth

```php
use Intervention\HttpAuth\Authenticator;

// create http basic auth
$auth = Authenticator::basic(
    'myUsername',
    'myPassword',
);
```

#### Create Authenticator Using HTTP Digest Auth

```php
use Intervention\HttpAuth\Authenticator;

// create http digest auth
$auth = Authenticator::digest(
    'myUsername',
    'myPassword',
);
```

### 2. Ask User for Credentials

After you created a HTTP authentication instance, you have to call `secure()`
to secure the resource. This results in a 401 HTTP response and the browser
asking for credentials.

```php
$auth->secure();
```

A character string can optionally be passed to the method. This is displayed if
authentication fails. Output from template engines can also be used here.

```php
$auth->secure('Sorry, you can not access this resource!');
```

Read more on how to [install](/v5/introduction/installation) or [use the package](/v5/api/authenticator).
