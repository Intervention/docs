# Installation
## Installation with Composer

[TOC]

## Server Requirements

Before you begin with the installation make sure that your server environment
supports the following requirements.

- PHP >= 8.2

## Installation

You can install this package quickly and easily with [Composer](https://getcomposer.org/).

Require the package via Composer:

```bash
$ composer require intervention/httpauth
```

After the installation you can start [using the authenticator](/v5/api/authenticator).

## Server Configuration

Although the configuration of the HTTP server should usually already be set
correctly, in rare cases it may be necessary to make adjustments.

### Apache

If you are using Apache and running PHP with CGI/FastCGI, check the server
configuration to make sure the [authorization headers are passed correctly to
PHP](https://support.deskpro.com/en/kb/articles/missing-authorization-headers-with-apache).
