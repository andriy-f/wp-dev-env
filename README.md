# Setup development environment

1. Copy `db.env.template` to `db.env` and change if needed.

2. Copy `sercrets-template` contents to `secrets` and **modify** secret files (fill in random passwords)

Helpful directives:

ini_set('display_errors', 0);
define('FS_METHOD', 'direct');

// Worpress recoomendtions for reverse proxy setup
if( strpos( $_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false )
  $_SERVER['HTTPS'] = 'on';