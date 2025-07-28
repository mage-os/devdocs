# How to add your own products-links providers (related, upsell, crossell)

[TOC]

## Introduction

This tutorial defines how to add your custom product link provider. We'll go through all the needed steps and code in order to build a custom module which will provide with such functionality.

## Prerequisites

Before proceeding with the below steps, please ensure you have a local installation of Mage-OS ready and running.

If you don't have it yet, please follow [installation instructions](/docs/{{version}}/installation-guide) in order to have Mage-OS ready for this tutorial.

## Step 1: build a custom module skeleton

We'll build the module under: `path-to-your-projects-root/app/code`.

First step is to create our module's vendor folder and module's folder under: `path-to-your-projects-root/app/code/MageOS/CustomProductLink`

Where `MageOS` is the vendor name and `CustomProductLink` the name of our module.

Then we'll create the 2 mandatory files so Mage-OS recognize our module:

`path-to-your-projects-root/app/code/MageOS/CustomProductLink/etc/module.xml`

Where `module.xml` will contain basic information about our module and its modules dependencies:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd"
>
    <module name="MageOS_CustomProductLink" >
        <sequence>
            <module name="Magento_Catalog"/>
        </sequence>
    </module>
</config>
```

`path-to-your-projects-root/app/code/MageOS/CustomProductLink/registration.php`

Where `registration.php` will contain the needed code to register our module under our Mage-OS project:

```php
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'MageOS_CustomProductLink',
    __DIR__
);
```

After having this completed, we should be able to activate our module, to do so, we need to go to a console and at the Mage-OS's root directory, run:

```shell
bin/magento module:enable MageOS_CustomProductLink
```

and we should see an output like below:

```shell
The following modules have been enabled:
- MageOS_CustomProductLink
```

This means that our new module has been correctly registered and enabled in our project.

## Step 2: creating data patch file to insert our custom link type in Mage-OS database tables

Before proceeding with this step, it's recommended checking your current database (especially if it's not a clean Mage-OS installation) to see what was the latest product link type inserted in order to reserve a new ID for our new custom link type.

To do so, connect to your database, navigate to table `catalog_product_link_type` and check for the highest `link_type_id` value.

In a fresh Mage-OS installation, there should be something like that:

```mysql
> select * from catalog_product_link_type;
+--------------+------------+
| link_type_id | code       |
+--------------+------------+
|            1 | relation   |
|            3 | super      |
|            4 | up_sell    |
|            5 | cross_sell |
+--------------+------------+
```

As we can see, the highest `link_type_id` is `5`, so we'll use `6` for our custom type.

Now, we're ready to create our data patch file. To do so, we need to create a data patch file under: `path-to-your-projects-root/app/code/MageOS/CustomProductLink/Setup/Patch/Data/AddCustomProductLink.php`

This file will insert the needed data to link tables so our custom product link type will be recognized by Mage-OS.

The file looks like below:

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Setup\Patch\Data;

use Magento\Framework\Setup\ModuleDataSetupInterface;
use Magento\Framework\Setup\Patch\DataPatchInterface;

class AddCustomProductLink implements DataPatchInterface
{
    private ModuleDataSetupInterface $moduleDataSetup;

    public function __construct(ModuleDataSetupInterface $moduleDataSetup)
    {
        $this->moduleDataSetup = $moduleDataSetup;
    }

    public static function getDependencies()
    {
        return [];
    }

    public function getAliases()
    {
        return [];
    }

    public function apply()
    {
        $this->moduleDataSetup->getConnection()->insertForce(
            $this->moduleDataSetup->getTable('catalog_product_link_type'),
            [
                'link_type_id' => 6,
                'code' => 'custom'
            ]
        );

        $this->moduleDataSetup->getConnection()->insertMultiple(
            $this->moduleDataSetup->getTable('catalog_product_link_attribute'),
            [
                [
                    'link_type_id' => 6,
                    'product_link_attribute_code' => 'position',
                    'data_type' => 'int'
                ]
            ]
        );
    }
}
```

After having this done, we should run:

```shell
bin/magento setup:upgrade
```

And if everything went well, we should see an output like below:

```mysql
> select * from catalog_product_link_type;
+--------------+------------+
| link_type_id | code       |
+--------------+------------+
|            1 | relation   |
|            3 | super      |
|            4 | up_sell    |
|            5 | cross_sell |
|            6 | custom     |
+--------------+------------+
```

Like explained above, we're using `6` for our `link_type_id`.

Also, you can add some attributes to the custom link type, we'll use `position` and `short_description` so you can see we can use different attribute types.

For now, 3 data types are allowed for these attributes, as there are 3 tables reserved for attribute types in the database: `catalog_product_link_attribute_decimal`, `catalog_product_link_attribute_varchar`, `catalog_product_link_attribute_int`.
