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

### Option: Install Magento with a Mage-OS Mirror
If you would prefer to use Magento instead of Mage-OS, you can do that by using this command instead:

```bash
composer create-project --repository-url=https://mirror.mage-os.org/ magento/project-community-edition
```

There are numerous mirror providers. You can see the full list and pick from others at
[https://mage-os.org/distribution/#magento-mirrors](https://mage-os.org/distribution/#magento-mirrors).

### Option: Add Magento Marketplace support
If you install Mage-OS, or Magento 2 using a
[Magento mirror](https://mage-os.org/distribution/#magento-mirrors), you will not have automatic access to
Magento / Adobe Commerce Marketplace. To install extensions from Marketplace, you need to configure
`repo.magento.com` as a composer repository. This will let you install any of the modules you may have
purchased from the Magento Marketplace.

It is also recommended that you either make use of Composer's
[repository prioritisation](https://getcomposer.org/doc/articles/repository-priorities.md#canonical-repositories) or
[repository filtering](https://getcomposer.org/doc/articles/repository-priorities.md#filtering-packages) features
(or both) to allow both the Mage-OS (or mirror) and Marketplace repositories to coexist in your project.

An example Composer repository configuration is given below:
```json
"repositories": {
    "mage-os": {
        "type": "composer",
        "url": "https://repo.mage-os.org/"
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

Please create a database in MySQL or MariaDB to contain your new Mage-OS or Magento installation.

For search engine Mage-OS supports Elasticsearch 7, Elasticsearch 8 and OpenSearch.

### Example command

```bash
php bin/magento setup:install \
    --db-host="localhost" \
    --db-name="magento_db" \
    --db-user="magento_user" \
    --db-password="password123" \
    --search-engine=opensearch \
    --opensearch-host=opensearch \
    --opensearch-port=9200 \
    --opensearch-index-prefix=magento2 \
    --opensearch-enable-auth=0 \
    --opensearch-timeout=15 \
    --admin-firstname="Admin" \
    --admin-lastname="User" \
    --admin-email="admin@example.com" \
    --admin-user="admin" \
    --admin-password="Admin123!" \
    --language="en_US" \
    --currency="USD" \
    --timezone="America/Chicago"
```

Some additional steps

Then set your secure and unsecure base url:

```bash
bin/magento config:set web/unsecure/base_url "https://www.example.com"
bin/magento config:set web/secure/base_url "https://www.example.com"

bin/magento config:set web/secure/use_in_frontend 1
bin/magento config:set web/secure/use_in_adminhtml 1
```

Enable web server url rewrites for SEO friendly urls:
```bash
bin/magento config:set web/seo/use_rewrites 1
```

Reindex all indexers and flush the cache
```bash
bin/magento indexer:reindex
bin/magento cache:flush
```

## Step 3: Enable the Magento 2 Cron Job

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
and customizing it to fit your needs. The `setup:install` command from Step 2 should have given you an admin URL.
Open that and enter the admin username and password you set to log in and start using your new site.

If you have any trouble installing Mage-OS, please reach out in the #help channel on http://chat.mage-os.org .
