---
description: Learn how to install Mage-OS with this comprehensive guide. Includes step-by-step instructions, prerequisites, system requirements, and troubleshooting tips for setting up your eCommerce platform.
keywords: Mage-OS installation, Mage-OS setup, Mage-OS prerequisites, eCommerce platform, system requirements, Mage-OS installation guide, Mage-OS documentation, install Mage-OS, Mage-OS troubleshooting.
communityNote: false
---
# Installation Guide for Mage-OS

[TOC]

## Introduction

This installation guide provides step-by-step instructions for installing Mage-OS on your server. The guide assumes
you have a basic understanding of programming concepts, specifically PHP and Magento 2. By following these instructions,
you will be able to successfully install Mage-OS and start building your online store.

## Prerequisites

Before installation, ensure your server fulfills the following requirements:

- PHP: 8.1 to 8.3
- Database: MySQL 8.0 or MariaDB 10.6
- Search Engine: Elasticsearch 7, 8, or OpenSearch 2.5+
- Web Server: Apache 2.4 or nginx 1.24
- Composer 2.7+

**Recommended (Optional):**

- RabbitMQ 3.11
- Redis 7.0
- Varnish 7.3

For AWS users, consider using [AWS ElastiCache]((https://aws.amazon.com/elasticache/)) and other services for
compatibility.

### Recommended software by version

| Software       | 1.1.0         | 1.0.6         | 1.0.5         | 1.0.4         |
|----------------|---------------|---------------|---------------|---------------|
| PHP            | 8.4           | 8.3           | 8.3           | 8.3           |
| Composer       | 2.8.8         | 2.7.4         | 2.7.4         | 2.7.4         |
| Database       | mariadb:11.4  | mariadb:10.6  | mariadb:10.6  | mariadb:10.6  |
| Search engine  | Os:2.19.1     | Es 8.11.4     | Es 8.11.4     | Es 8.11.4     |
| RabbitMQ       | 4.0           | 3.13          | 3.13          | 3.13          |
| Redis          | 7.2           | 7.2           | 7.2           | redis:7.2     |
| Varnish        | 7.6           | 7.5           | 7.5           | 7.5           |
| Nginx          | 1.26          | 1.26          | 1.26          | 1.26          |
| OS             | ubuntu-latest | ubuntu-latest | ubuntu-latest | ubuntu-latest |
| Release Date   | 2025-04-15    | 2025-02-12    | 2024-10-09    | 2024-08-20    |

| Software       | 1.0.3         | 1.0.2         | 1.0.1         | 1.0.0         |
|----------------|---------------|---------------|---------------|---------------|
| PHP            | 8.3           | 8.3           | 8.1           | 8.1           |
| Composer       | 2.7.4         | 2.7.4         | 2.2.21        | 2.2.21        |
| Database       | mariadb:10.6  | mariadb:10.6  | mysql:8.0     | mysql:8.0     |
| Search engine  | Es 8.11.4     | Es 8.11.4     | Es 8.5.3      | Es 8.5.3      |
| RabbitMQ       | 3.13          | 3.9           | 3.9           | 3.9           |
| Redis          | 7.2           | 7.2           | 7.0           | 7.0           |
| Varnish        | 7.5           | 7.5           | 7.3           | 7.3           |
| Nginx          | 1.26          | 1.26          | 1.22          | 1.22          |
| OS             | ubuntu-latest | ubuntu-latest | ubuntu-latest | ubuntu-latest |
| Release Date   | 2024-07-23    | 2024-07-18    | 2023-10-11    | 2023-10-10    |

ES - Elasticsearch
OS - Opensearch

## Step 1: Download Mage-OS

The first step in the installation process is to download the Mage-OS package. You can use Composer to install it.

To download Mage-OS using Composer, open your command line interface and navigate to your project directory. Then, run
the following command:

```shell
composer create-project --repository-url=https://repo.mage-os.org/ mage-os/project-community-edition .
```

This command will download the latest version of Mage-OS and all its dependencies.

### Option: Install Magento with a Mage-OS Mirror

If you would prefer to use Magento instead of Mage-OS, you can do that by using this command instead:

```shell
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

An example Composer repository configuration, adding repo.magento.com for `vendorC` and `vendorE` packages only:

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

## Step 2: Installation

Post Composer package installation, your directory should resemble:

```shell
YourWorkingDirectory
|- CHANGELOG.md
|- LICENSE.txt
|- app/
|- composer.json
|- generated/
|- nginx.conf.sample
|- pub/
|- vendor/
|- COPYING.txt
|- LICENSE_AFL.txt
|- auth.json.sample
|- composer.lock
|- grunt-config.json.sample
|- package.json.sample
|- setup/
|- Gruntfile.js.sample
|- SECURITY.md
|- bin/
|  |- magento
|- dev/
|- lib/
|- phpserver/
|- var/
```

You can now install Magento's Database and set up the connected services, like Elasticsearch/OpenSearch or Redis.
Although Magento doesn't require Redis, it is highly recommended to use it up front for your Session and Config Cache
Storage. To install Magento, we can use Magento's built-in Command-Line-Tool `bin/magento`.

The following command installs the Magento Database, configures Elasticsearch as the Search Engine, RabbitMQ for async
processes, and uses Redis to store sessions, config cache, and the full page cache in separate internal databases. 
All configuration can be adjusted later. Run `bin/magento setup:install --help` to see the full list of available
parameters.

Please create a database in MySQL or MariaDB to contain your new Mage-OS or Magento installation.

```shell
bin/magento setup:install \
    --db-host=DATABASE_HOST \
    --db-name=DATABASE_NAME \
    --db-user=DATABASE_USER \
    --db-password=DATABASE_PASSWORD \
    --base-url=https://www.example.com/ \
    --base-url-secure=https://www.example.com/ \
    --backend-frontname=BACKEND_FRONTNAME \
    --use-secure=1 \
    --use-secure-admin=1 \
    --use-rewrites=1
```

### Some additional parameters

#### Redis
If you have installed Redis, you can add the following parameters to the above `bin/magento setup:install` command

```shell
    --session-save=redis \
    --session-save-redis-host=REDIS_HOST \
    --session-save-redis-port=REDIS_PORT \
    --session-save-redis-db=0 \
    --session-save-redis-max-concurrency=20 \
    --cache-backend=redis \
    --cache-backend-redis-server=REDIS_HOST \
    --cache-backend-redis-port=REDIS_PORT \
    --cache-backend-redis-db=1 \
    --page-cache=redis \
    --page-cache-redis-server=REDIS_HOST \
    --page-cache-redis-port=REDIS_PORT \
    --page-cache-redis-db=2
```

#### RabbitMQ 
If you have installed RabbitMQ, you can add the following parameters to the above `bin/magento setup:install` command

```shell
    --amqp-host=RABBIT_MQ_HOST \
    --amqp-port=RABBIT_MQ_PORT \
    --amqp-user=RABBIT_MQ_USER \
    --amqp-password=RABBIT_MQ_PASSWORD
```

#### Elasticsearch
If you have installed Elasticsearch, you can add the following parameters to the above `bin/magento setup:install` command

```shell
    --search-engine=elasticsearch7 \
    --elasticsearch-host=ELASTICSEARCH_HOST \
    --elasticsearch-port=ELASTICSEARCH_PORT
```

#### Opensearch
If you have installed Opensearch, you can add the following parameters to the above `bin/magento setup:install` command

```shell
    --search-engine=opensearch \
    --opensearch-host=OPENSEARCH_HOST \
    --opensearch-port=OPENSEARCH_PORT \
    --opensearch-index-prefix=OPENSEARCH_INDEX_PREFIX \
    --opensearch-timeout=15
```
#### Admin User
If you want to create an Admin User during the installation, you can add the following parameters to the above `bin/magento setup:install` command

```shell
    --admin-firstname=ADMIN_FIRSTNAME \
    --admin-lastname=ADMIN_LASTNAME \
    --admin-email=ADMIN_EMAIL \
    --admin-user=ADMIN_USER \
    --admin-password=ADMIN_PASSWORD
```

#### Store Configuration
If you want to configure some base store settings, you can add the following parameters to the above `bin/magento setup:install` command

```shell
    --language=languageCode_countryCode \
    --currency=CURRENCY \
    --timezone=TIMEZONE
```
Example:
```shell
    --language=en_US \
    --currency=USD \
    --timezone=America/New_York
```

### Some additional steps

After the installation completes:

set _developer mode_ (only if you are in local environment)
```shell
bin/magento deploy:mode:set developer
```

reindex all indexes and flush the cache
```shell
bin/magento indexer:reindex
bin/magento cache:flush
```

## Step 3: Enable the Magento 2 Cron Job

Mage-OS relies on a cron job to perform scheduled tasks, such as indexing, cache flushing, and sending email
notifications. To enable the Mage-OS cron job, you need to add a cron job entry to your server.

Open your command line interface and run the following command:

```shell
bin/magento cron:install
```

Verify the command's success with:

```shell
crontab -l
```

You should see output like:

```shell
#~ MAGENTO START 69dd2b02e1f3a65918182048ea4e29979a849d8942e8f53ed20a4bf10e529b36
* * * * * /usr/bin/php /var/www/html/bin/magento cron:run 2>&1 | grep -v "Ran jobs by schedule" >> /var/www/html/var/log/magento.cron.log
#~ MAGENTO END 69dd2b02e1f3a65918182048ea4e29979a849d8942e8f53ed20a4bf10e529b36
```

## Conclusion

Congratulations! You have successfully installed Mage-OS on your server. You can now start building your online store
and customizing it to fit your needs. The `setup:install` command from Step 2 should have given you an admin URL.
Open that and enter the admin username and password you set to log in and start using your new site.

If you have any trouble installing Mage-OS, please reach out in the #help channel on 
[http://chat.mage-os.org](http://chat.mage-os.org).


## Option: Local Development with Warden

If you're working on MacOS or Linux and want to install Magento locally, we highly recommend the docker-based dev
environment [warden](https://warden.dev/). Follow the steps below after
you [installed warden](https://docs.warden.dev/installing.html).

After you run through the steps below, you will have fully configured Magento 2 running locally with Redis, OpenSearch,
RabbitMQ, MariaDB, SSL, PHP, Xdebug, and Varnish.

> **Note**
> The steps below are provided by the official warden documentation.

**Create a new environment**

```shell
warden env-init YOUR_PROJECTNAME magento2
```

**Sign an SSL certificate for use with the project**

```shell
warden sign-certificate YOUR_PROJECTNAME.test
```

**Spin up the environment**

```shell
warden env up
```

**Access your shell**

```shell
warden shell
```

**Ensure `pub/static` is available**

```shell
mkdir -p pub/static
```

**Install the Application**

```shell
bin/magento setup:install \
     --backend-frontname=backend \
     --amqp-host=rabbitmq \
     --amqp-port=5672 \
     --amqp-user=guest \
     --amqp-password=guest \
     --db-host=db \
     --db-name=magento \
     --db-user=magento \
     --db-password=magento \
     --search-engine=opensearch \
     --opensearch-host=opensearch \
     --opensearch-port=9200 \
     --opensearch-index-prefix=magento2 \
     --opensearch-enable-auth=0 \
     --opensearch-timeout=15 \
     --http-cache-hosts=varnish:80 \
     --session-save=redis \
     --session-save-redis-host=redis \
     --session-save-redis-port=6379 \
     --session-save-redis-db=2 \
     --session-save-redis-max-concurrency=20 \
     --cache-backend=redis \
     --cache-backend-redis-server=redis \
     --cache-backend-redis-db=0 \
     --cache-backend-redis-port=6379 \
     --page-cache=redis \
     --page-cache-redis-server=redis \
     --page-cache-redis-db=1 \
     --page-cache-redis-port=6379
```

**Configure the Application**

```shell
bin/magento config:set --lock-env web/unsecure/base_url "https://${TRAEFIK_SUBDOMAIN}.${TRAEFIK_DOMAIN}/"
bin/magento config:set --lock-env web/secure/base_url "https://${TRAEFIK_SUBDOMAIN}.${TRAEFIK_DOMAIN}/"
bin/magento config:set --lock-env web/secure/offloader_header X-Forwarded-Proto
bin/magento config:set --lock-env web/secure/use_in_frontend 1
bin/magento config:set --lock-env web/secure/use_in_adminhtml 1
bin/magento config:set --lock-env web/seo/use_rewrites 1
bin/magento config:set --lock-env system/full_page_cache/caching_application 2
bin/magento config:set --lock-env system/full_page_cache/ttl 604800
bin/magento config:set --lock-env catalog/search/enable_eav_indexer 1
bin/magento config:set --lock-env dev/static/sign 0
bin/magento deploy:mode:set -s developer
bin/magento cache:disable block_html full_page
bin/magento indexer:reindex
bin/magento cache:flush
bin/magento cache:enable
```

**Set up an admin user incl. 2FA**

Magento requires admin users to use 2FA. Although the use of 2FA is highly recommended on production sites, developers
often find it tedious to set it up locally. Mark Shust created a widely
used [Magento Extension](https://github.com/markshust/magento2-module-disabletwofactorauth) to disable 2FA **locally**.

> **Warning**
> Don't disable 2FA in internet-facing installations. Your system's protection will suffer otherwise.

```shell
ADMIN_PASS="$(pwgen -n1 16)"
ADMIN_USER=localadmin

bin/magento admin:user:create \
    --admin-password="${ADMIN_PASS}" \
    --admin-user="${ADMIN_USER}" \
    --admin-firstname="Local" \
    --admin-lastname="Admin" \
    --admin-email="${ADMIN_USER}@example.com"
printf "u: %s\np: %s\n" "${ADMIN_USER}" "${ADMIN_PASS}"

## Configure 2FA provider
OTPAUTH_QRI=
# Python 2: TFA_SECRET=$(python -c "import base64; print base64.b32encode('$(pwgen -A1 128)')" | sed 's/=*$//')
# Python 3:
TFA_SECRET=$(python3 -c "import base64; print(base64.b32encode(bytearray('$(pwgen -A1 128)', 'ascii')).decode('utf-8'))" | sed 's/=*$//')
OTPAUTH_URL=$(printf "otpauth://totp/%s%%3Alocaladmin%%40example.com?issuer=%s&secret=%s" \
    "${TRAEFIK_SUBDOMAIN}.${TRAEFIK_DOMAIN}" "${TRAEFIK_SUBDOMAIN}.${TRAEFIK_DOMAIN}" "${TFA_SECRET}"
)

bin/magento config:set --lock-env twofactorauth/general/force_providers google
bin/magento security:tfa:google:set-secret "${ADMIN_USER}" "${TFA_SECRET}"

printf "%s\n\n" "${OTPAUTH_URL}"
printf "2FA Authenticator Codes:\n%s\n" "$(oathtool -s 30 -w 10 --totp --base32 "${TFA_SECRET}")"

segno "${OTPAUTH_URL}" -s 4 -o "pub/media/${ADMIN_USER}-totp-qr.png"
printf "%s\n\n" "https://${TRAEFIK_SUBDOMAIN}.${TRAEFIK_DOMAIN}/media/${ADMIN_USER}-totp-qr.png?t=$(date +%s)"
```

**Set up an admin user without 2FA**

```shell
ADMIN_PASS="$(pwgen -n1 16)"
ADMIN_USER=localadmin

bin/magento admin:user:create \
    --admin-password="${ADMIN_PASS}" \
    --admin-user="${ADMIN_USER}" \
    --admin-firstname="Local" \
    --admin-lastname="Admin" \
    --admin-email="${ADMIN_USER}@example.com"
printf "u: %s\np: %s\n" "${ADMIN_USER}" "${ADMIN_PASS}"
```

You should now be able to access your site under `https://app.YOUR_PROJECTNAME.test/`.
