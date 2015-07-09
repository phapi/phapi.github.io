---
title: Directory structure
excerpt: Where should all the files go and what are all those directories doing?
---

## Directory structure
The [phapi/phapi-configuration](https://github.com/phapi/phapi-configuration) project includes everything you need to set up a simple hello world example. **[Download the latest version](https://github.com/phapi/phapi-configuration/archive/master.zip)** of the package and extract it to an empty directory.

The first thing to do after you've downloaded and extracted the file is to install all dependencies (including the Phapi Framework) using composer:

```shell
$ composer install
```

This will install the Phapi Framework and all it's dependencies to a new directory named <code>vendor</code>.

Your project structure should look like this:

```
- app
  - configuration           < Folder containing all configuration
    - default               < Default configuration, should not be edited
      - container.php
      - pipeline.php
      - settings.php
    - middleware.php        < This is where we list all the middleware we want to use.
    - routes.php            < Contains all the routes that points to endpoints
    - settings.php          < This is where all your custom configuration should go
  - endpoint                < This is where all your endpoints should be
    - Home.php
  - logs                    < Save your logs here
  - public_html             < Web server root, configure your web server to point to this folder
    - index.php             < The starting point, this file includes all the needed configuration.
- vendor                    < Contains Phapi and dependencies
```
