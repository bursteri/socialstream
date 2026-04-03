# Socialstream

Community-maintained fork of [joelbutcher/socialstream](https://github.com/joelbutcher/socialstream) with **Laravel 13** support.

OAuth for Laravel Breeze, Jetstream and Filament -- simplified.

## Why this fork?

The original Socialstream was archived when Laravel dropped Breeze and Jetstream from the official installer. But plenty of projects still use these stacks and need a solid OAuth integration. This fork keeps the package alive and compatible with the latest Laravel releases.

## Requirements

- PHP 8.3+
- Laravel 11, 12 or 13
- Laravel Socialite 5.18+

## Installation

```bash
composer require bursteri/socialstream
```

The package auto-discovers its service provider. No manual registration needed.

## Supported stacks

- **Laravel Breeze** (Blade, Inertia with Vue/React)
- **Laravel Jetstream** (Livewire, Inertia)
- **Filament**

## Supported providers

Bitbucket, Facebook, GitHub, GitLab, Google, LinkedIn, LinkedIn OpenID, Slack, Twitter (OAuth 1.0 and 2.0).

You can also register custom providers via Socialite's built-in extension system.

## Setup

Publish the config, migrations, actions and routes:

```bash
php artisan socialstream:install
```

Then add providers to `config/socialstream.php`:

```php
use JoelButcher\Socialstream\Providers;

'providers' => [
    Providers::google(),
    Providers::github(),
],
```

And configure your credentials in `config/services.php` as you normally would with Socialite:

```php
'github' => [
    'client_id' => env('GITHUB_CLIENT_ID'),
    'client_secret' => env('GITHUB_CLIENT_SECRET'),
    'redirect' => '/oauth/github/callback',
],
```

## Features

Toggle features in `config/socialstream.php`:

```php
use JoelButcher\Socialstream\Features;

'features' => [
    Features::createAccountOnFirstLogin(),
    Features::generateMissingEmails(),
    Features::globalLogin(),
    Features::authExistingUnlinkedUsers(),
    Features::rememberSession(),
    Features::providerAvatars(),
    Features::refreshOAuthTokens(),
],
```

## Migrating from joelbutcher/socialstream

1. Replace the package in `composer.json`:
   ```bash
   composer remove joelbutcher/socialstream
   composer require bursteri/socialstream
   ```
2. That's it. The namespace (`JoelButcher\Socialstream`) is unchanged, so all your imports, config references, and published actions continue to work.

## Original documentation

For detailed usage guides, refer to the original docs at [docs.socialstream.dev](https://docs.socialstream.dev).

## Credits

- [Joel Butcher](https://github.com/joelbutcher) -- original author
- [All contributors](https://github.com/bursteri/socialstream/contributors)

## License

MIT. See [LICENSE.md](LICENSE.md).