---
title: "Authenticator"
subtitle: "Using the HTTP Authenticator"
lead: "Learn how to use the HTTP Authenticator library for securing resources with Basic or Digest authentication in PHP. Leveraging secure vaults and configuring custom failure messages. Includes code examples for effortless integration."
sort: 0
---

[TOC]

## Creating the Authenticator

**I strongly recommend using a library like [PHP
dotenv](https://github.com/vlucas/phpdotenv) to store the credentials and keep
usernames and passwords out of version control.**


### Create Authenticator by Passing the Vault

#### Create by Class Constructor

> public Authenticator::__construct(VaultInterface $vault): Authenticator

Create a new authenticator instance by passing the desired type of
authorization vault in the class constructor.

#### Parameters

| Name | Type | Description |
| - | - | - |
| vault | VaultInterface | Instance of VaultInterface. Usually instance `BasicVault::class` or `DigestVault::class` |

#### Example

```php
use Intervention\HttpAuth\Authenticator;
use Intervention\HttpAuth\Vaults\BasicVault

// create vault first
$vault = new BasicVault(
    'myUsername',
    'myPassword',
    'Secured Area',
);

// create authenticator
$auth = new Authenticator($vault);
```

#### Create by Static Helper

> public Authenticator::withVault(VaultInterface $vault): Authenticator

Create a new authenticator instance by calling the static factory
method directly and passign the vault instance directly.

#### Parameters

| Name | Type | Description |
| - | - | - |
| vault | VaultInterface | Instance of VaultInterface. Usually instance `BasicVault::class` or `DigestVault::class` |

#### Example

```php
use Intervention\HttpAuth\Authenticator;
use Intervention\HttpAuth\Vaults\DigestVault

// create vault first
$vault = new DigestVault('myUsername', 'myPassword');

// create authenticator with vault
$auth = Authenticator::withVault($vault);
```


### Create Authenticator with Static Factory Methods

#### Basic Auth Factory Method

> public Authenticator::basic(string $username, string $password, string $realm = 'Secured Area'): Authenticator

Create a new basic auth authenticator instance by calling the static factory
method directly and passign the credentials as well as the name of the
resource.

#### Parameters

| Name | Type | Description |
| - | - | - |
| username | string | Username for securing the resource |
| password | string | Password for securing the resource |
| realm | string | Name of the secured resource |

#### Example

```php
use Intervention\HttpAuth\Authenticator;

// create authenticator
$auth = Authenticator::basic(
    'myUsername',
    'myPassword',
    'Secured Area',
);
```

#### Digest Auth Factory Method

> public Authenticator::digest(string $username, string $password, string $realm = 'Secured Area'): Authenticator

Create a new digest auth authenticator instance by calling the static factory
method directly and passign the credentials as well as the name of the
resource.

#### Parameters

| Name | Type | Description |
| - | - | - |
| username | string | Username for securing the resource |
| password | string | Password for securing the resource |
| realm | string | Name of the secured resource |

#### Example

```php
use Intervention\HttpAuth\Authenticator;

// create authenticator
$auth = Authenticator::digest(
    'myUsername',
    'myPassword',
    'Secured Area',
);
```




## Securing the Resource

> public Authenticator::secure(?string $message = null): void

After you created a HTTP authenticator instance, you have to call `secure()` to
secure the resource by checking for credentials. Otherwise nothing will happen.

By calling `Authenticator::secure()` the server ask the user for a username and
a password. If the credentials are entered incorretly a HTTP status code 401 is
sent and the use will not be able to access the resource.

The method optionally accepts a character string as content that is displayed
to the user if the verification fails. HTML content can also be transferred
here or output from template engines can be used.

#### Parameters

| Name | Type | Description |
| - | - | - |
| message | string or null | Content that is displayed to the user if authentication fails. |

#### Example

```php
use Intervention\HttpAuth\Authenticator;

// creating the authenticator and checking credentials can be a one liner
Authenticator::basic('myUsername', 'myPassword')->secure();
```

```php
use Intervention\HttpAuth\Authenticator;

// create auth
$auth = Authenticator::digest('myUsername', 'myPassword', 'Secure Area');

// secure resource with custom message
$auth->secure('Sorry, you can not access this resource!');
