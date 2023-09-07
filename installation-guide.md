# Installation Guide for Magento 2

[TOC]

## Introduction

This installation guide provides step-by-step instructions for installing Magento 2 on your server. The guide assumes
you have a basic understanding of programming concepts, specifically PHP and Magento 2. By following these instructions,
you will be able to successfully install Magento 2 and start building your online store.

## Prerequisites

Before proceeding with the installation, please ensure that your server meets the following prerequisites:

- PHP 8.1 or later
- MySQL 8.1 or later
- Apache or Nginx web server
- Composer 2

## Step 1: Download Magento 2

The first step in the installation process is to download the Magento 2 package. You can download the package from the
official Magento website or use Composer to install it.

To download Magento 2 using Composer, open your command line interface and navigate to your project directory. Then, run
the following command:

```bash
composer create-project --repository-url=... .
```

This command will download the latest version of Magento 2 and all its dependencies.

### Using Mage-OS Mirrors
When opting to install Magento 2 using one of the
[Mage-OS mirror repositories](https://mage-os.org/distribution/#magento-mirrors), you will still need to configure
`repo.magento.com` as one of your Composer repositories in order to download and install any of the modules you may have
purchased from the Magento marketplace.

It is also recommended that you either make use of Composer's
[repository prioritisation](https://getcomposer.org/doc/articles/repository-priorities.md#canonical-repositories) or
[repository filtering](https://getcomposer.org/doc/articles/repository-priorities.md#filtering-packages) features
(or both) to allow both the Mage-OS mirror and Magento repositories to coexist in your project.

An example Composer repository configuration is given below:
```json
"repositories": {
    "mage-os-mirror": {
        "type": "composer",
        "url": "https://mirror.mage-os.org/",
        "only": [
            "magento/*",
            "paypal/*",
            "vendorA/*",
            "vendorB/module-b"
        ]
    },
    "magento-marketplace": {
        "type": "composer",
        "url": "https://repo.magento.com",
        "only": [
            "vendorC/module-d",
            "vendorE/*"
        ]
    },
},
```

## Step 2: Configure the Database

Magento 2 requires a database to store its data. Before proceeding with the installation, you need to configure the
database settings.

Start by creating a new database for your Magento 2 installation. You can use a tool like phpMyAdmin or the command line
to create the database.

Next, open the `app/etc/env.php` file in your Magento 2 installation directory. Look for the following section:

```php
'db' => [
    'table_prefix' => '',
    'connection' => [
        'default' => [
            'host' => 'localhost',
            'dbname' => 'magento',
            'username' => 'root',
            'password' => '',
            'active' => '1'
        ]
    ]
],
```

Update the database settings according to your environment. Replace `'localhost'` with the hostname of your database
server, `'magento'` with the name of your database, `'root'` with the username, and `''` with the password. Leave
the `'table_prefix'` field empty unless you want to specify a prefix for your Magento tables.

## Step 3: Run the Installation Wizard

Once the database is configured, you can run the Magento 2 installation wizard. Open your web browser and navigate to
the URL where you placed your Magento 2 files.

You will be greeted with the Magento 2 installation wizard. Follow the on-screen instructions to complete the
installation process. Make sure to provide the necessary information, such as your store name, admin email, username,
and password.

During the installation, Magento 2 will perform various database operations and install the necessary tables. After the
installation is complete, you will be redirected to the Magento admin panel.

## Step 4: Enable the Magento 2 Cron Job

Magento 2 relies on a cron job to perform scheduled tasks, such as indexing, cache flushing, and sending email
notifications. To enable the Magento 2 cron job, you need to add a cron job entry to your server.

Open your command line interface and run the following command:

```bash
crontab -e
```

This command will open the cron job configuration file. Add the following line to the file:

```bash
* * * * * <path-to-php> <magento-root>/bin/magento cron:run >> <magento-root>/var/log/cron.log
```

Replace `<path-to-php>` with the path to your PHP binary and `<magento-root>` with the path to your Magento 2
installation directory.

Save the file and exit the editor. The cron job will now run every minute and execute the Magento 2 cron tasks.

## Conclusion

Congratulations! You have successfully installed Magento 2 on your server. You can now start building your online store
and customizing it to fit your needs.

Please refer to the official Magento 2 documentation for more information on how to configure and use Magento 2.
