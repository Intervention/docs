---
title: "Installation"
subtitle: "Installation with Composer"
lead: "Learn how to install Intervention Zodiac for PHP with Composer"
sort: 1
---

## Server Requirements

Before you begin with the installation make sure that your server environment supports the following requirements.

PHP >= 8.2

## Installation

Use [Composer](https://getcomposer.org) for the installation by running the following command.

```bash
composer require intervention/zodiac
```

Although the library is **framework agnostic** it comes with a service provider
for the [Laravel Framework](https://www.laravel.com/). Which will be discovered
automatically and registers the calculator into your installation.

After the installation you can start [using the calculator](/v6/api/calculator).
