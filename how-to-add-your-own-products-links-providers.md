# How to add your own products-links providers (related, upsell, crossell)

[TOC]

## Introduction

This tutorial defines how to add your custom product link provider. We'll go through all the needed steps and code in order to build a module which will provide with such functionality.

## Prerequisites

Before proceeding with the below steps, please ensure you have a local installation of Mage-OS ready and running.

If you don't have it yet, please follow [installation instructions](/docs/{{version}}/installation-guide) in order to have Mage-OS ready for this tutorial.

## Step 1: build a module skeleton

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
use MageOS\CustomProductLink\Model\Product;
use MageOS\CustomProductLink\Model\Product\Link;

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
                'link_type_id' => Link::LINK_TYPE_ACCESSORY,
                'code' => Product::CUSTOM_LINK_CODE
            ]
        );

        $this->moduleDataSetup->getConnection()->insertMultiple(
            $this->moduleDataSetup->getTable('catalog_product_link_attribute'),
            [
                [
                    'link_type_id' => Link::LINK_TYPE_ACCESSORY,
                    'product_link_attribute_code' => 'position',
                    'data_type' => 'int'
                ]
            ]
        );
    }
}
```

we need to declare:

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Model;

class Product
{
    public const CUSTOM_LINK_CODE = 'accessory';
}
```

and the last file is:

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Model\Product;

class Link extends \Magento\Catalog\Model\Product\Link
{
    public const LINK_TYPE_ACCESSORY = 6;

    /**
     * @return $this
     */
    public function useAccessoryLinks()
    {
        $this->setLinkTypeId(self::LINK_TYPE_ACCESSORY);
        return $this;
    }
}

```

After having this done, we should run:

```shell
bin/magento setup:upgrade
```

And if everything went well, we should see the accessory link an output like below:

```mysql
> select * from catalog_product_link_type;
+--------------+------------+
| link_type_id | code       |
+--------------+------------+
|            1 | relation   |
|            3 | super      |
|            4 | up_sell    |
|            5 | cross_sell |
|            6 | accessory  |
+--------------+------------+
```

Like explained above, we're using `6` for our `link_type_id`.

Also, you can add some attributes to the accessory link type, we'll use `position` and `short_description` so you can see we can use different attribute types.

For now, 3 data types are allowed for these attributes, as there are 3 tables reserved for attribute types in the database: `catalog_product_link_attribute_decimal`, `catalog_product_link_attribute_varchar`, `catalog_product_link_attribute_int`.

To set up a custom product link, we’ll need to inject certain dependencies into the core link provider classes. For this, create the following di.xml file.

`path-to-your-projects-root/app/code/MageOS/etc/di.xml`

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Catalog\Model\Product\CopyConstructor\Composite">
        <arguments>
            <argument name="constructors" xsi:type="array">
                <item name="accessory" xsi:type="string">MageOS\CustomProductLink\Model\Product\CopyConstructor\Accessory</item>
            </argument>
        </arguments>
    </type>
    <type name="Magento\Catalog\Model\Product\LinkTypeProvider">
        <arguments>
            <argument name="linkTypes" xsi:type="array">
                <item name="accessory" xsi:type="const">MageOS\CustomProductLink\Model\Product\Link::LINK_TYPE_ACCESSORY</item>
            </argument>
        </arguments>
    </type>
    <type name="Magento\Catalog\Model\ProductLink\CollectionProvider">
        <arguments>
            <argument name="providers" xsi:type="array">
                <item name="accessory" xsi:type="object">MageOS\CustomProductLink\Model\ProductLink\CollectionProvider\Accessory</item>
            </argument>
        </arguments>
    </type>
</config>
```

create the Accessory class:

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Model\Product\CopyConstructor;

use Magento\Catalog\Model\Product;
use Magento\Catalog\Model\Product\CopyConstructorInterface;
use Magento\Catalog\Model\Product\Link;

class Accessory implements CopyConstructorInterface
{

    public function build(Product $product, Product $duplicate)
    {
        $data = [];
        $attributes = [];

        $link = $product->getLinkInstance();
        $link->useAccessoryLinks();
        foreach ($link->getAttributes() as $attribute) {
            if (isset($attribute['code'])) {
                $attributes[] = $attribute['code'];
            }
        }
        /** @var Link $link  */
        foreach ($product->getAccessoryLinkCollection() as $link) {
            $data[$link->getLinkedProductId()] = $link->toArray($attributes);
        }

        $duplicate->setAccessoryLinkData($data);
    }
}
```

The class `MageOS\CustomProductLink\Model\Product\Link` was created earlier, so no additional work is need it.
Now we need to create the class responsible for the collection provider `MageOS\CustomProductLink\Model\ProductLink\CollectionProvider\Accessory`

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Model\ProductLink\CollectionProvider;

use Magento\Catalog\Model\Product;
use Magento\Catalog\Model\ProductLink\CollectionProviderInterface;

class Accessory implements CollectionProviderInterface
{
    protected $accessoryModel;

    public function __construct(
        \MageOS\CustomProductLink\Model\Accessory $accessoryModel
    ) {
        $this->accessoryModel = $accessoryModel;
    }

    /**
     * {@inheritdoc}
     */
    public function getLinkedProducts(Product $product)
    {
        return $this->accessoryModel->getAccessoryProducts($product);
    }
}
```

The two classes `MageOS\CustomProductLink\Model\Product\CopyConstructor\Accessory` and `MageOS\CustomProductLink\Model\ProductLink\CollectionProvider\Accessory` are using the class `\MageOS\CustomProductLink\Model\Accessory`. The class is providing data from the database, so let's implement it:

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Model;

use Magento\Catalog\Model\Product;
use Magento\Catalog\Model\ResourceModel\Product\Link\Collection;
use Magento\Framework\DataObject;
use MageOS\CustomProductLink\Model\Product\Link;

class Accessory extends DataObject
{
    /**
     * Product link instance
     *
     * @var Product\Link
     */
    protected $linkInstance;

    /**
     * Accessory constructor.
     * @param Link $productLink
     */
    public function __construct(
        Link $productLink
    ) {
        $this->linkInstance = $productLink;
    }

    /**
     * Retrieve link instance
     *
     * @return  Product\Link
     */
    public function getLinkInstance()
    {
        return $this->linkInstance;
    }

    /**
     * Retrieve array of Accessory products
     *
     * @param Product $currentProduct
     * @return array
     */
    public function getAccessoryProducts(Product $currentProduct)
    {
        if (!$this->hasAccessoryProducts()) {
            $products = [];
            $collection = $this->getAccessoryProductCollection($currentProduct);
            foreach ($collection as $product) {
                $products[] = $product;
            }
            $this->setAccessoryProducts($products);
        }
        return $this->getData('accessory_products');
    }

    /**
     * Retrieve accessory products identifiers
     *
     * @param Product $currentProduct
     * @return array
     */
    public function getAccessoryProductIds(Product $currentProduct)
    {
        if (!$this->hasAccessoryProductIds()) {
            $ids = [];
            foreach ($this->getAccessoryProducts($currentProduct) as $product) {
                $ids[] = $product->getId();
            }
            $this->setAccessoryProductIds($ids);
        }
        return $this->getData('accessory_product_ids');
    }

    /**
     * Retrieve collection accessory product
     *
     * @param Product $currentProduct
     * @return \Magento\Catalog\Model\ResourceModel\Product\Link\Product\Collection
     */
    public function getAccessoryProductCollection(Product $currentProduct)
    {
        $collection = $this->getLinkInstance()->useAccessoryLinks()->getProductCollection()->setIsStrongMode();
        $collection->setProduct($currentProduct);
        return $collection;
    }

    /**
     * Retrieve collection accessory link
     *
     * @param Product $currentProduct
     * @return Collection
     */
    public function getAccessoryLinkCollection(Product $currentProduct)
    {
        $collection = $this->getLinkInstance()->useAccessoryLinks()->getLinkCollection();
        $collection->setProduct($currentProduct);
        $collection->addLinkTypeIdFilter();
        $collection->addProductIdFilter();
        $collection->joinAttributes();
        return $collection;
    }
}
```

We are almost there, now we need to display the accessory items associated with the product, create `etc/adminhtml/di.xml` file:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <virtualType name="Magento\Catalog\Ui\DataProvider\Product\Form\Modifier\Pool">
        <arguments>
            <argument name="modifiers" xsi:type="array">
                <item name="accessory" xsi:type="array">
                    <item name="class" xsi:type="string">MageOS\CustomProductLink\Ui\DataProvider\Product\Form\Modifier\Accessory</item>
                    <item name="sortOrder" xsi:type="number">120</item>
                </item>
            </argument>
        </arguments>
    </virtualType>
</config>
```

Then we need to create the class that will just defined in the admin di.xml file: `\MageOS\CustomProductLink\Ui\DataProvider\Product\Form\Modifier\Accessory`

```php
<?php

declare(strict_types=1);

namespace MageOS\CustomProductLink\Ui\DataProvider\Product\Form\Modifier;

use Magento\Catalog\Ui\DataProvider\Product\Form\Modifier\Related;
use Magento\Ui\Component\Form\Fieldset;

class Accessory extends Related
{
    public const DATA_SCOPE_ACCESSORY = 'accessory';
    /**
     * @var string
     */
    private static $previousGroup = 'search-engine-optimization';
    /**
     * @var int
     */
    private static $sortOrder = 90;
    /**
     * {@inheritdoc}
     */
    public function modifyMeta(array $meta)
    {
        $meta = array_replace_recursive(
            $meta,
            [
                static::GROUP_RELATED => [
                    'children' => [
                        $this->scopePrefix . static::DATA_SCOPE_ACCESSORY => $this->getAccessoryFieldset()
                    ],
                    'arguments' => [
                        'data' => [
                            'config' => [
                                'label' => __('Related Products, Up-Sells, Cross-Sells and Accessory'),
                                'collapsible' => true,
                                'componentType' => Fieldset::NAME,
                                'dataScope' => static::DATA_SCOPE,
                                'sortOrder' => $this->getNextGroupSortOrder(
                                    $meta,
                                    self::$previousGroup,
                                    self::$sortOrder
                                ),
                            ],
                        ],
                    ],
                ],
            ]
        );
        return $meta;
    }
    /**
     * Prepares config for the Custom type products fieldset
     *
     * @return array
     */
    protected function getAccessoryFieldset()
    {
        $content = __(
            'Custom type products are shown to customers in addition to the item the customer is looking at.'
        );
        return [
            'children' => [
                'button_set' => $this->getButtonSet(
                    $content,
                    __('Add Accessory Products'),
                    $this->scopePrefix . static::DATA_SCOPE_ACCESSORY
                ),
                'modal' => $this->getGenericModal(
                    __('Add Accessory Products'),
                    $this->scopePrefix . static::DATA_SCOPE_ACCESSORY
                ),
                static::DATA_SCOPE_ACCESSORY => $this->getGrid($this->scopePrefix . static::DATA_SCOPE_ACCESSORY),
            ],
            'arguments' => [
                'data' => [
                    'config' => [
                        'additionalClasses' => 'admin__fieldset-section',
                        'label' => __('Accessory Products'),
                        'collapsible' => false,
                        'componentType' => Fieldset::NAME,
                        'dataScope' => '',
                        'sortOrder' => 90,
                    ],
                ],
            ]
        ];
    }
    /**
     * Retrieve all data scopes
     *
     * @return array
     */
    protected function getDataScopes()
    {
        return [
            static::DATA_SCOPE_ACCESSORY
        ];
    }
}
```
