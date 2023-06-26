# Basic Configuration in Magento 2

- [Global Configuration: env.php](#global-configuration-env.php)
- [Application Configuration: config.php](#application-configuration-config.php)
- [Module Configuration: config.xml](#module-configuration-config.xml)

Magento 2, a highly flexible PHP-based e-commerce framework, provides a wealth of configuration options that allow you
to tailor your e-commerce platform precisely to your needs. This guide aims to provide you with a comprehensive
understanding of Magento 2's basic configuration.

## Global Configuration: env.php

Magento's global configuration is located in the `app/etc/env.php` file. This file contains settings that apply to the
entire Magento application, such as backend frontname, install date, crypt key, session save location, and more.

### Example

```php
return [
  'backend' =>
    [
        'frontName' => 'admin',
    ],
  'install' =>
    [
        'date' => 'Fri, 25 Jun 2023 19:25:14 +0000',
    ],
  // ...
];
```

In the above example, `'frontName' => 'admin'`, is the URL segment for the admin panel.

## Application Configuration: config.php

Magento's `config.php` file is located in the same directory as `env.php` (`app/etc/`). This file is responsible for
managing the list of installed modules and their `enable/disable` status.

```php
return [
  'modules' => [
    'Magento_Store' => 1,
    'Magento_AdminNotification' => 1,
    //...
  ],
];
```

In this configuration, `'Magento_Store'` and `'Magento_AdminNotification'` modules are enabled as indicated by `'1'`. 
If a module is disabled, it would be indicated by `'0'`.

## Module Configuration: config.xml

Each module in Magento 2 has its own `config.xml` file which is found in the `etc` directory of the respective module.
This file is used to manage module-specific configurations, such as default values for the module's settings.

### Example

Let's take a look at an example configuration in a `config.xml` file:

```xml

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Store:etc/config.xsd">
    <default>
        <catalog>
            <frontend>
                <list_per_page>12</list_per_page>
            </frontend>
        </catalog>
    </default>
</config>
```

In this example, we have the `<list_per_page>12</list_per_page>` configuration inside the `<catalog><frontend>` path.
This particular setting dictates the default number of products displayed per page on the product list.

Remember: After modifying a module's `config.xml file`, it's necessary to clear Magento's cache (System > Tools > Cache
Management) to apply the changes.

Before adjusting these configurations, remember that they can significantly impact your application's functionality and
behavior. It's highly recommended that you have a thorough understanding of Magento 2's architecture and always test
these changes in a development or staging environment before applying them to a live store. This ensures stability and
can prevent unintended effects on the end-user experience.
