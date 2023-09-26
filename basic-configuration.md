# Basic Configuration

[TOC]

## Introduction

Magento 2, a versatile eCommerce platform, offers extensive configurability to meet the needs of developers. This
document discusses the fundamental configuration in Magento 2, focusing on `app/etc/env.php`, `app/etc/config.php`,
`core_config_data` table, `config.xml`, and managing configuration programmatically.

## Environment Configuration in `app/etc/env.php`

The `app/etc/env.php` file is pivotal for environment-specific configurations. It stores settings such as database
connection information, backend front name, cryptographic key, and more.

### Database Connection

The `db` section in `app/etc/env.php` contains the database connection information. It is used by Magento to connect to
the database. The following snippet shows the default database connection settings:

```php
// app/etc/env.php
return [
    // ...
    'db' => [
        'connection' => [
            'default' => [
                'host' => 'YOUR_DATABASE_HOST',
                'dbname' => 'YOUR_DATABASE_NAME',
                'username' => 'YOUR_DATABASE_USER',
                'password' => 'YOUR_DATABASE_PASSWORD',
                'model' => 'mysql4',
                'engine' => 'innodb',
                'initStatements' => 'SET NAMES utf8;',
                'active' => '1',
                'driver_options' => [
                    // Add your PDO driver options here. @see https://www.php.net/manual/en/ref.pdo-mysql.php
                ]
            ]
        ],
        'table_prefix' => '' // Add a table prefix here if you are sharing this database with other applications. Not recommended...
    ],
    // ...
];
```

### Backend Front Name

The `backend` section in `app/etc/env.php` contains the backend front name. It is used by Magento to access the backend
area. The following snippet shows the default backend front name:

```php
// app/etc/env.php
return [
    // ...
    'backend' => [
        'frontName' => 'admin' // To lower the risk of brute-force attacks, change this to something unique.
    ],
    // ...
];
```

### Cryptographic Key

The `crypt` section in `app/etc/env.php` contains the cryptographic key. It is used by Magento to encrypt sensitive data
such as passwords and credit card numbers. The following snippet shows the default cryptographic key:

```php
// app/etc/env.php
return => [
    'crypt' => [
        'key' => 'YOUR_CRYPT_KEY'
    ]
];
```

> **Note**  
> You can use multiple versions of the cryptographic key. This is useful when you need to change the cryptographic key
> without invalidating existing encrypted data. For more information,
> see [Encryption key management](https://devdocs.mage-os.org/docs/main/best-practices-for-secure-development).



