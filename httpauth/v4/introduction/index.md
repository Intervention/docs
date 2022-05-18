# Intervention HttpAuth
## HTTP Authentication Management

Intervention HttpAuth is a library to manage HTTP basic & digest authentication.

### Code Example

The handling is easy. You just have to create an authenticator with your desired settings and call the `secure()` method to check for given credentials

```php
use Intervention\HttpAuth\HttpAuth;

// create authenticator
$auth = new HttpAuth();
$auth->withType('digest');
$auth->withRealm('Secure Realm');
$auth->withCredentials('admin', 'secret');

// check for credentials
$auth->secure();
```

The library comes with several static factory methods to create the authenticator.

```php
use Intervention\HttpAuth\HttpAuth;

// create by array
$auth = HttpAuth::make([
   'type' => 'basic',
   'realm' => 'Secure Resource',
   'username' => 'admin',
   'password' => 'secret',
]);
```

Read more on how to [install](/v4/introduction/installation) or [use the package](/v4/introduction/usage)
