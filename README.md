## WordPress development environment

## Setup development environment

1. Copy `db.env.template` to `db.env` and change if needed.

1. Copy `secrets-template` contents to `secrets` and **modify** secret files (fill in random passwords)

1. Copy `./reverse-proxy/conf/Caddyfile.template` to `./reverse-proxy/conf/Caddyfile`

1. if you plan to use tls (ssl), create docker/podman secrets 
```sh
podman secret create localhost.crt PATH
podman secret create localhost.key PATH
```

In `./reverse-proxy/conf/Caddyfile`:

  - remove `auto_https off` 
  - uncomment `https_port 8443`
  - uncomment `tls /run/secrets/localhost.crt /run/secrets/localhost.key`

## Sometimes helpful directives (add to wp-config.php)

```php
ini_set('display_errors', 0);
define('FS_METHOD', 'direct');
```

## WordPress recommendation for reverse proxy setup

Add those to `wp-config.php`.

```php
if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
  $_SERVER['HTTPS'] = 'on';
}
```

**wp-cli**

```sh
su -c "wp --info" -s /bin/bash www-data
```