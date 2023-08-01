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
- PHP: Version 8.1 or later, with necessary extensions for Magento 2.

## Software Stack

### Web Server

Choose either Apache or Nginx as your web server. Here's an example of installing and configuring Apache:

```bash
$ sudo apt update
$ sudo apt install apache2
```

After installation, configure Apache by editing the main configuration file located at `/etc/apache2/apache2.conf`.

### Database Server

Choose either MySQL or MariaDB as your database server. Here's an example of installing and configuring MySQL:

```bash
$ sudo apt update
$ sudo apt install mysql-server
```

During the installation, you will be prompted to set the root password for MySQL. Make sure to choose a strong password.

### PHP

Magento 2 requires PHP 8.1 or later. Here's an example of installing PHP and necessary extensions:

```bash
$ sudo apt update
$ sudo apt install php8.1 php8.1-cli php8.1-fpm php8.1-mysql php8.1-curl php8.1-gd php8.1-intl php8.1-mbstring php8.1-xml php8.1-zip
```

After installation, update the PHP configuration file located at `/etc/php/8.1/apache2/php.ini` and make the necessary
changes.

## Server Setup

### Installing and Configuring the Web Server

1. Install the chosen web server software (Apache or Nginx) as described in the previous section.
2. Configure the web server to listen on the appropriate IP address and port.
3. Set up virtual hosts to point to your Magento 2 installation directory.
4. Enable necessary modules and configurations, such as SSL/TLS, if required.

### Setting up the Database Server

1. Install the chosen database server software (MySQL or MariaDB) as described in the previous section.
2. Secure the database server by running the security script provided by the database software.
3. Create a new database and database user for Magento 2, and grant the necessary privileges to the user.

### Configuring PHP

1. Update the PHP configuration file (`php.ini`) to set the necessary values.
2. Adjust PHP settings related to memory limits, file uploads, and execution time as needed.
3. Make sure the required PHP extensions for Magento 2 are enabled.

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

For Nginx, add the following configuration snippet within the `server` block:

```nginx
location / {
    try_files $uri $uri/ /index.php?$args;
}
```

## Conclusion

With this documentation, you should now have a server set up and properly configured to host PHP-based applications,
specifically Magento 2. Make sure to follow best practices for security and performance optimization. Remember to keep
your server software and dependencies up to date to ensure a stable and secure environment for your applications. Happy
coding!
