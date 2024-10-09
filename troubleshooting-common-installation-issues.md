---
description: Discover solutions to common Magento 2 installation issues with the Mage-OS troubleshooting guide. Learn to resolve database connection errors, file permissions issues, missing PHP extensions, and more.
keywords: Mage-OS, Magento 2 installation issues, troubleshooting Magento, database connection error, file permissions, missing PHP extensions, memory limit exceeded, Magento installation fixes, Magento server setup, cache clearing
---
# Troubleshooting Common Installation Issues

[TOC]

This documentation aims to provide solutions to common installation issues encountered while setting up a PHP-based
e-commerce platform, specifically Magento 2. The instructions assume that you have a basic understanding of programming
concepts and the Magento 2 framework.

## Server Requirements

Before troubleshooting any installation issues, make sure your server meets the minimum requirements for running Magento
2. These requirements include PHP version, extensions, and server configurations. Consult the official Magento 2
documentation or the system requirements provided by your hosting provider for the exact specifications.

## Invalid Credentials for Database Connection

One common installation issue occurs when Magento 2 fails to connect to the database due to incorrect credentials. To
resolve this, verify that the database credentials specified in the `app/etc/env.php` file are correct. For example:

```php
'db' => [
    'connection' => [
        'default' => [
            'host' => 'localhost',
            'dbname' => 'magento',
            'username' => 'magento_user',
            'password' => 'magento_password',
            'active' => '1',
        ],
    ],
],
```

Ensure the host, dbname, username, and password values match those provided by your database administrator or hosting
provider.

## File and Directory Permissions

Magento 2 requires specific file and directory permissions to function properly. Incorrect permissions can result in
installation issues, such as blank pages or access denied errors. Here are some general guidelines:

- All directories should have permissions set to `770`.
- All files should have permissions set to `660`.
- The `var`, `pub/static`, and `generated` directories, as well as their subdirectories, should have permissions set
  to `777`.

To set permissions, navigate to your Magento 2 root directory and execute the following commands:

```bash
chmod -R 770 var pub/static generated
chmod 660 app/etc/env.php
```

This ensures the necessary read, write, and execute permissions are set correctly.

## Missing Required PHP Extensions

Magento 2 relies on various PHP extensions to function properly. If you encounter an error indicating a missing
extension, you need to install it. Here's an example:

```
PHP Extension xsl is not loaded.
```

In this case, you would need to install the XSL extension for PHP. The exact method varies depending on your operating
system and PHP setup. For example, on Ubuntu, you can install it using the following command:

```bash
sudo apt-get install php-xsl
```

Refer to your operating system's documentation or consult with your hosting provider to install the required extensions.

## Memory Limit Exceeded

During installation or operation, Magento 2 may encounter memory limit errors. This typically occurs due to insufficient
memory allocated to PHP. To resolve this, you can increase the memory limit by editing the PHP configuration
file (`php.ini`).

Locate the `memory_limit` directive and adjust its value to a higher limit. For example:

```
memory_limit = 512M
```

Save the file and restart your web server to apply the changes.

## Clearing Cache and Generated Files

If you encounter unexpected issues during installation or after making changes to your Magento 2 installation, it's
often helpful to clear the cache and generated files. Magento 2 provides command-line tools for this purpose.

To clear the cache, run the following command from your Magento 2 root directory:

```bash
bin/magento cache:clean
```

To regenerate static files, run the following command:

```bash
bin/magento setup:static-content:deploy
```

These commands ensure that any cached data or outdated generated files are removed and regenerated.

## Unexpected Issues with Custom CLI Commands

Magento 2 users may encounter unexpected issues with custom CLI commands from third parties during project setups, test executions, or deployments. A common error arises during the magento setup command, indicating the `magento.flag` does not exist. This error often occurs due to premature database calls, causing a stalled system installation.

**Preventive Strategies**

- Avoid resource-consuming operations: Do not make DB/API calls in the `__construct` methods of CLI command classes.
- Avoid unavailable resources: Do not use resources in `__construct` that might not be available during runtime.
- Use Proxies: If you cannot control the code, inject a Proxy using di configs.

**Automated Proxy Injection**

For extensive projects, identifying problematic CLI commands can be challenging. The [run-as-root/magento-cli-auto-proxy](https://github.com/run-as-root/magento-cli-auto-proxy) package automates the proxy injection process, eliminating early resource access errors and speeding up `php bin/magento` and `php bin/magento setup:install` executions.


## Conclusion

This documentation has provided solutions to common installation issues encountered while setting up Magento 2. By
following these troubleshooting steps, you should be able to address most problems you may encounter during the
installation process. Remember to consult the official Magento 2 documentation or seek assistance from the Magento
community if you encounter any issues that remain unresolved.
