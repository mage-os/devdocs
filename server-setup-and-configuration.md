# Server Setup and Configuration Documentation

[TOC]

This documentation provides step-by-step instructions for setting up and configuring a server for hosting PHP-based
applications, specifically focusing on Magento 2. It assumes that the reader has some familiarity with programming, PHP,
and Magento 2.

## Server Requirements

Before setting up the server, make sure it meets the following minimum requirements:

- Operating System: Linux, preferably CentOS or Ubuntu.
- Web Server: Apache or Nginx.
- Database Server: MySQL or MariaDB.
- PHP: Version 8.1 or later, with the necessary extensions for Magento 2.
- Search Engine: Opensearch ( recommended ) or Elasticsearch
- composer

## Software Stack

### Web Server

Choose either Apache or Nginx as your web server. Here's an example of installing and configuring Apache:

```bash
$ sudo apt update
$ sudo apt install apache2
$ a2enmod rewrite headers ssl expires brotli
```

After installation, configure Apache by editing the main configuration file located at `/etc/apache2/apache2.conf`.

Most of the Apache2 settings are done by Magentos .htaccess file for Apache2. There are some things you should consider.

* Make sure to enable deflate and brotli for compression.
Set up an SSL certificate and redirect to SSL. You can use [let's encrypt](https://letsencrypt.org/de/) or similar services for a free SSL certificate.
* Make sure, to use a PHP process manager like php-fpm or nginx-unit and set up enough PHP processes for your expected traffic.

As nginx can't parse the .htaccess file, you need to set up with a magento configuration. You can use the one [provided by magento](https://github.com/mage-os/mageos-magento2/blob/2.4-develop/nginx.conf.sample).

### Database Server

Choose either MySQL or MariaDB as your database server. Here's an example of installing and configuring MySQL:

```bash
$ sudo apt update
$ sudo apt install mysql-server
```

During the installation, you will be prompted to set the root password for MySQL. Make sure to choose a strong password.

Make sure to use MySQL 8.0 or later.

If your operating system, doesn't support MySQL 8.0, install the software  repositories provided by MySQL.

### PHP

Magento 2 requires PHP 8.1 or later. Here's an example of installing PHP and the necessary extensions:

```bash
$ sudo apt update
$ sudo apt install php8.2 php8.2-apcu php8.2-amqp php8.2-bcmath php8.2-bz2 php8.2-cli php8.2-common php8.2-curl php8.2-dba php8.2-fpm php8.2-gd php8.2-igbinary php8.2-imagick php8.2-imap php8.2-intl php8.2-mbstring php8.2-memcached php8.2-msgpack php8.2-mysql php8.2-opcache php8.2-phpdbg php8.2-redis php8.2-soap php8.2-sqlite3 php8.2-xml php8.2-zip
```

After installation, update the PHP configuration file located at `/etc/php/8.2/fpm/php.ini` and make the necessary
changes.

To keep up to date with PHP, you should take a look at the repository provided by [Ondřej Surý](https://deb.sury.org/)

### composer

Fetch the latest composer.phar for https://getcomposer.org/download/

### searchengine

By default, Magento requires Opensearch or Elasticsearch as a search engine. 

As Elasticsearch changed its licensing model to a non open-source license with 7.17, it won't be provided by most providers of managed hostings in most version.

Instead, you can use the [opensearch](https://opensearch.org/) fork which provides updates under the Apache 2.0 license. You can download it, from the [opensearch homepage](https://opensearch.org/downloads.html)

## Server Setup

### Installing and Configuring the Web Server

1. Install the chosen web server software (Apache or Nginx) as described in the previous section.
2. Configure the web server to listen on the appropriate IP address and port.
3. Set up virtual hosts to point to the pub folder inside your Magento 2 installation directory.
4. Enable necessary modules and configurations, such as SSL/TLS, if required.

### Setting up the database Server

1. Install the chosen database server software (MySQL or MariaDB) as described in the previous section.
2. Secure the database server by running the security script provided by the database software.
3. Create a new database and database user for Magento 2, and grant the necessary privileges to the user.
4. It's recommended to increase the InnoDB Buffer pool to make use of your available memory on production servers.

### Configuring PHP

1. Update the PHP configuration file (`php.ini`) to set the necessary values.
2. Adjust PHP settings related to memory limits, file uploads, and execution time as needed.
3. Make sure the required PHP extensions for Magento 2 are enabled.
4. For production servers, make sure to increase the PHP Opcache for performance.
   

## Magento 2 Specific Configuration

### File and Directory Permissions

Magento 2 requires specific file and directory permissions for proper functioning. Here's an example of setting
permissions:

```bash
$ cd /var/www/html/magento2
$ find var generated vendor pub/static pub/media app/etc -type f -exec chmod u+w {} +
$ find var generated vendor pub/static pub/media app/etc -type d -exec chmod u+w {} +
$ chmod u+x bin/magento
```

### URL Rewrites

To enable user-friendly URLs in Magento 2, URL rewriting must be enabled. Here's an example of configuring URL rewrites
for Apache:

```bash
$ sudo a2enmod rewrite
$ sudo service apache2 restart
```

For Nginx, there is nothing special to do.

### Optional components

In addition to the requirements, there are some optional components you can install:

* You can install varnish as an FPC before magento, for high-performance shops.
* You can move sessions and magento cache inside a Redis instance. You should use this when you plan to use more than one server.
* You can use RabbitMQ as an alternative message queue.
You can move the lock provider from the database to zookeeper. 


## Conclusion

With this documentation, you should now have a server set up and properly configured to host PHP-based applications,
specifically Magento 2. Make sure to follow best practices for security and performance optimization. Remember to keep
your server software and dependencies up to date to ensure a stable and secure environment for your applications. Happy
coding!
