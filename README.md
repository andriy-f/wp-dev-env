# Setup development environment

1. Copy .devcontainers/db.env.template to .devcontainers/db.env and change if needed

Helpful directives:

ini_set('display_errors', 0);
define('FS_METHOD', 'direct');

// Worpress recoomendtions for reverse proxy setup
if( strpos( $_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false )
  $_SERVER['HTTPS'] = 'on';