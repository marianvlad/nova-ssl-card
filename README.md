# Nova SSL Card

[![Latest Version on Packagist](https://img.shields.io/packagist/v/marianvlad/nova-ssl-card.svg?style=flat-square)](https://packagist.org/packages/marianvlad/nova-ssl-card)
[![Total Downloads](https://img.shields.io/packagist/dt/marianvlad/nova-ssl-card.svg?style=flat-square)](https://packagist.org/packages/marianvlad/nova-ssl-card)

Get details about ssl certificates inside a Nova card.

## Installation

You can install the package in to a Laravel app that uses [Nova](https://nova.laravel.com) via composer:

```bash
composer require marianvlad/nova-ssl-card
```

Next up, you must register the card Nova. This is typically done in the `cards` method of the `NovaServiceProvider`.

```php
// in app/Providers/NovaServiceProvider.php

// ...

public function cards()
{
    return [
        // ...
        new \Marianvlad\NovaSslCard\NovaSslCard,
    ];
}
```
 
## Usage

By default the card will show SSL certificate details about current domain
where you have installed Nova but you can configure for any domain name

```php
// in app/Providers/NovaServiceProvider.php

// ...

public function cards()
{
    return [
        new \Marianvlad\NovaSslCard\NovaSslCard, // current domain
        // or
        new \Marianvlad\NovaSslCard\NovaSslCard('domain.tld'),
    ];
}
```

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.