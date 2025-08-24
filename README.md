## WordPress development environment

## Setup development environment

1. Copy `db.env.template` to `db.env` and change if needed.

2. Copy `secrets-template` contents to `secrets` and **modify** secret files (fill in random passwords)

## Helpful directives

ini_set('display_errors', 0);
define('FS_METHOD', 'direct');

## WordPress recommendation for reverse proxy setup

Add those to `wp-config.php`.

```php
if( strpos( $_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false )
  $_SERVER['HTTPS'] = 'on';
```