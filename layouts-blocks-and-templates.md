# Layouts, Blocks, and Templates Documentation

[TOC]

## Introduction

In Magento 2, layouts, blocks, and templates form the backbone of the presentation layer of your online store.
Understanding how these components work together is crucial for customizing the appearance and functionality of your
Magento store. This documentation provides an in-depth overview of layouts, blocks, and templates, including their
definitions, relationships, and usage examples.

## Layouts

### Definition

Layouts in Magento 2 are XML files that define the structure and content of a page. They specify the positioning and
rendering of blocks and containers within a page. Layout files are located in the `app/design/frontend/`
or `app/design/adminhtml/` directory of your Magento installation.

### Structure

A layout file consists of a `<layout>` root node, which can contain multiple `<block>` and `<container>` nodes.
The `<block>` nodes represent individual blocks of content, while the `<container>` nodes define areas within the layout
where blocks can be dynamically added.

### Usage Example

Consider a scenario where you want to add a banner to the homepage of your Magento store. To achieve this, you would
create a custom layout file named `cms_index_index.xml` within your theme's layout directory. Within this file, you
would define a new block that corresponds to your banner, specifying its template and other attributes.

```xml
<layout xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Magento\Framework\View\Element\Template" name="custom_banner"
                   template="Vendor_Module::banner.phtml" after="cms_page">
                <arguments>
                    <argument name="banner_text" xsi:type="string">Welcome to our store!</argument>
                </arguments>
            </block>
        </referenceContainer>
    </body>
</layout>
```

In this example, we've created a block named `custom_banner` and associated it with the `Vendor_Module::banner.phtml`
template. We've also passed a custom argument `banner_text` to the block, which can be accessed within the template.

## Blocks

### Definition

Blocks in Magento 2 are PHP classes that handle the business logic and rendering of specific sections of a webpage. They
encapsulate data and functionality, which can be accessed and manipulated within the associated templates. Blocks are
instantiated and configured within layout files using the `<block>` nodes.

### Usage Example

Suppose you want to create a block that displays a list of recently added products. You would create a custom PHP block
class, `RecentProducts`, which extends the `Magento\Framework\View\Element\Template` class. Within this class, you would
define a method, `getRecentProducts()`, that retrieves the necessary data and returns it to the template.

```php
<?php

namespace Vendor\Module\Block;

use Magento\Framework\View\Element\Template;

class RecentProducts extends Template
{
    protected $productCollectionFactory;

    public function __construct(
        Template\Context $context,
        \Magento\Catalog\Model\ResourceModel\Product\CollectionFactory $productCollectionFactory,
        array $data = []
    ) {
        $this->productCollectionFactory = $productCollectionFactory;
        parent::__construct($context, $data);
    }

    public function getRecentProducts()
    {
        $collection = $this->productCollectionFactory->create();
        $collection->addAttributeToSelect('*')
            ->setOrder('created_at', 'DESC')
            ->setPageSize(5);
            
        return $collection;
    }
}
```

Now, in your layout file, you can add the `RecentProducts` block to the desired container.

```xml
<block class="Vendor\Module\Block\RecentProducts" name="recent_products"
       template="Vendor_Module::recent_products.phtml"/>
```

In the associated template file, `recent_products.phtml`, you can access the data returned by the `getRecentProducts()`
method using the `$block` object.

```php
<?php
/** @var \Vendor\Module\Block\RecentProducts $block */

$recentProducts = $block->getRecentProducts();

foreach ($recentProducts as $product) {
    // Display product details
}
```

## Templates

### Definition

Templates in Magento 2 are PHP files that handle the presentation logic of a block. They define the HTML structure and
styling for a specific block. Templates are associated with blocks within layout files using the `template` attribute of
the `<block>` nodes.

### Usage Example

Consider the previous example of the `RecentProducts` block. In order to display the list of recent products, you would
create a template file named `recent_products.phtml` within your theme's template directory. Inside this file, you would
write the necessary HTML and PHP code to render the list.

```html+php
<?php
/** @var \Vendor\Module\Block\RecentProducts $block */
$recentProducts = $block->getRecentProducts();
?>

<div class="recent-products">
    <h2>Recently Added Products</h2>
    <ul>
        <?php foreach ($recentProducts as $product): ?>
            <li>
                <a href="<?php echo $block->getProductUrl($product); ?>"><?php echo $product->getName(); ?></a>
                <span class="price"><?php echo $product->getPrice(); ?></span>
            </li>
        <?php endforeach; ?>
    </ul>
</div>
```

In this template, we iterate over the `$recentProducts` array and generate the necessary HTML markup for each product.
We can access the product data and methods provided by the block using the `$block` object.

## Conclusion

Understanding the concepts of layouts, blocks, and templates is essential for customizing the appearance and
functionality of your Magento 2 store. Layouts define the structure of a page, blocks handle business logic and
rendering, and templates handle the presentation logic. By leveraging these components effectively, you can create a
highly customizable and visually appealing online store.
