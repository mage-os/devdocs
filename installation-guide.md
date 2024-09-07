# Installation Guide for Mage-OS

[TOC]

## Introduction

This installation guide provides step-by-step instructions for installing Mage-OS on your server. The guide assumes
you have a basic understanding of programming concepts, specifically PHP and Magento 2. By following these instructions,
you will be able to successfully install Mage-OS and start building your online store.

## Prerequisites

Before proceeding with the installation, please ensure that your server meets the following prerequisites:

- PHP 8.1 or later
- MySQL 8.1 or later
- Apache or Nginx web server
- Composer 2

## Step 1: Download Mage-OS

The first step in the installation process is to download the Mage-OS package. You can use Composer to install it.

To download Mage-OS using Composer, open your command line interface and navigate to your project directory. Then, run
the following command:

```bash
composer create-project --repository-url=https://repo.mage-os.org/ mage-os/project-community-edition .
```

This command will download the latest version of Mage-OS and all its dependencies.

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

## Step 2: Run install from command line

The bin/magento setup:install command is a vital part of the Mage-OS installation process. It automates the setup of a new Mage-OS instance by configuring necessary files, databases, and services. This command is commonly used in server environments to initialize Mage-OS after code deployment or during the installation of a fresh Mage-OS instance.

```bash
php bin/magento setup:install [options]
```

This command requires several options to properly configure the environment. It sets up the database connection, initializes admin credentials, configures base URLs, and installs required modules.

### Example command

```bash
php bin/magento setup:install \
    --base-url="https://www.example.com/" \
    --db-host="localhost" \
    --db-name="magento_db" \
    --db-user="magento_user" \
    --db-password="password123" \
    --admin-firstname="Admin" \
    --admin-lastname="User" \
    --admin-email="admin@example.com" \
    --admin-user="admin" \
    --admin-password="Admin123!" \
    --language="en_US" \
    --currency="USD" \
    --timezone="America/Chicago" \
    --use-rewrites="1"
```

## Step 4: Enable the Magento 2 Cron Job

Mage-OS relies on a cron job to perform scheduled tasks, such as indexing, cache flushing, and sending email
notifications. To enable the Mage-OS cron job, you need to add a cron job entry to your server.

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

Save the file and exit the editor. The cron job will now run every minute and execute the Mage-OS cron tasks.

## Conclusion

Congratulations! You have successfully installed Mage-OS on your server. You can now start building your online store
and customizing it to fit your needs.

Please refer to the official Mage-OS documentation for more information on how to configure and use Mage-OS.
