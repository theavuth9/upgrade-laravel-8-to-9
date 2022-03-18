# How to Upgrade Laravel 8 to Laravel 9

### 1. Check the version in `composer.json`
- change `laravel`:
```php
"laravel/framework": "^8.x" to "laravel/framework": "^9.0"
```

- change `nunomaduro/collision`:
```php
"nunomaduro/collision": "^5.x" to "nunomaduro/collision": "^6.1"
```

- relace `facade/ignition`:
```php
"facade/ignition": "xx" to "spatie/laravel-ignition": "^1.0"
```

### 2. Fixes proxy
- remove `fideloper/proxy` from `composer.json`
- change in `app/Http/Middleware/TrustProxies.php` from `use Fideloper\Proxy\TrustProxies as Middleware` to `use Illuminate\Http\Middleware\TrustProxies as Middleware`
- make sure in `app/Http/Middleware/TrustProxies.php`
```php
// Before...

protected $headers = Request::HEADER_X_FORWARDED_ALL;

// After...

protected $headers =
    Request::HEADER_X_FORWARDED_FOR |
    Request::HEADER_X_FORWARDED_HOST |
    Request::HEADER_X_FORWARDED_PORT |
    Request::HEADER_X_FORWARDED_PROTO |
    Request::HEADER_X_FORWARDED_AWS_ELB;
```
- well done, run
```php
composer update
```

### Done
