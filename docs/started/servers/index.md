---
layout: docs
title: Web servers
excerpt: Learn how to configure your web server
---

## Web servers

## Nginx configuration
Your nginx configuration should contain this code (please note that you might have other lines of codes in the <code>location</code> block):

```
location / {
  try_files $uri /$uri /index.php?$args;
}
```

This assumes that Phapi's index.php is located in the folder that is specified as <code>root</code> in the nginx configuration. Example:

```
root /www/phapi/app/public_html;
```

## Apache configuration
Place the .htaccess file in the same directory as your index.php. Make sure that your virtual host is configured to point to the directory. The .htaccess file should contain this code:

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]
```

Make sure your virtual host is configured with the <code>AllowOverride</code> option set to All so that the .htaccess rewrite rules can be used:

```
AllowOverride All
```
