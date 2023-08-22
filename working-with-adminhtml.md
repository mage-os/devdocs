# Adminhtml Documentation

[TOC]

This documentation provides a comprehensive guide to working with `adminhtml` in Magento 2. `adminhtml` is the
administrative interface of Magento, which allows administrators to manage different aspects of the website, such as
products, orders, customers, and more.

## Introduction <a name="introduction"></a>

The `adminhtml` area in Magento 2 follows the Model-View-Controller (MVC) architectural pattern, just like the frontend.
Understanding the components of adminhtml and how they interact with each other is crucial for developing custom admin
functionalities.

## Creating a Custom Adminhtml Module <a name="creating-a-custom-adminhtml-module"></a>

To create a custom adminhtml module, you need to follow these steps:

1. Create the required module directories and files.
2. Declare the module in `app/etc/config.php`.
3. Enable the module using the command line or the Magento Admin Panel.
4. Create admin routes, controllers, layouts, blocks, grids, forms, and menus as per your requirements.

## Admin Routes <a name="admin-routes"></a>

Admin routes are used to map URLs to controllers in the admin area. They define the structure of the URL and the
corresponding controller action.

To create an admin route, define the route in `adminhtml/routes.xml` in your custom module:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="admin">
        <route id="your_route_id" frontName="your_front_name">
            <module name="Your_Module" before="Magento_Backend"/>
        </route>
    </router>
</config>
```

After defining the admin route, you can access it using the following
URL: `/admin/adminhtml/your_front_name/controller/action`.

## Controllers <a name="controllers"></a>

Controllers in adminhtml handle the request and response for a specific admin route. They execute the business logic and
interact with models and other components to fulfill the request.

To create a controller, extend the `Magento\Backend\App\Action` class and define your actions:

```php
namespace Your\Module\Controller\Adminhtml\Controller;

use Magento\Backend\App\Action;

class YourController extends Action
{
    public function execute()
    {
        // Your controller logic here
    }
}
```

## Layouts <a name="layouts"></a>

Layouts define the structure and composition of the adminhtml pages. They control the placement of blocks and define the
appearance of the page.

To create a layout file, create `your_module_controller_action.xml` in `Your/Module/view/adminhtml/layout/`:

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Your\Module\Block\Adminhtml\YourBlock" name="your_block_name"
                   template="Your_Module::your_template.phtml"/>
        </referenceContainer>
    </body>
</page>
```

## Blocks <a name="blocks"></a>

Blocks in adminhtml are responsible for generating and rendering HTML content. They contain the logic and data required
to display the information on the admin page.

To create a block, extend the `Magento\Backend\Block\Template` class and define your block:

```php
namespace Your\Module\Block\Adminhtml;

use Magento\Backend\Block\Template;

class YourBlock extends Template
{
    // Your block logic here
}
```

## Grids <a name="grids"></a>

Grids are used to display tabular data in the adminhtml. They provide sorting, filtering, and pagination
functionalities.

To create a grid, extend the `Magento\Backend\Block\Widget\Grid\Container` class and define your grid:

```php
namespace Your\Module\Block\Adminhtml;

use Magento\Backend\Block\Widget\Grid\Container;

class YourGrid extends Container
{
    // Your grid logic here
}
```

## Forms <a name="forms"></a>

Forms in adminhtml are used to collect and save data. They allow administrators to enter and edit information through
input fields, dropdowns, checkboxes, and more.

To create a form, extend the `Magento\Backend\Block\Widget\Form\Container` class and define your form:

```php
namespace Your\Module\Block\Adminhtml;

use Magento\Backend\Block\Widget\Form\Container;

class YourForm extends Container
{
    // Your form logic here
}
```

## Menus <a name="menus"></a>

Menus in adminhtml provide navigation and organization of different sections and pages. They allow administrators to
access different functionalities easily.

To add a custom menu item, create `menu.xml` in `Your/Module/etc/adminhtml/`:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Backend:etc/menu.xsd">
    <menu>
        <add id="Your_Module::your_menu_id" title="Your Menu Title" module="Your_Module" sortOrder="10"
             resource="Your_Module::your_acl_resource"/>
        <add id="Your_Module::your_submenu_id" title="Your Submenu Title" parent="Your_Module::your_menu_id"
             module="Your_Module" sortOrder="10" action="your_route_id/controller/action"
             resource="Your_Module::your_acl_resource"/>
    </menu>
</config>
```

## ACL (Access Control List) <a name="acl"></a>

The ACL in adminhtml controls the access and permissions for different admin users. It defines which users can perform
specific actions or access certain pages.

To define an ACL, create `acl.xml` in `Your/Module/etc/adminhtml/`:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Acl/etc/acl.xsd">
    <acl>
        <resources>
            <resource id="Magento_Backend::admin">
                <resource id="Your_Module::your_acl_resource" title="Your ACL Title" sortOrder="10"/>
            </resource>
        </resources>
    </acl>
</config>
```

## Conclusion <a name="conclusion"></a>

Working with `adminhtml` in Magento 2 requires a good understanding of its components and their relationships. This
documentation aimed to provide a comprehensive overview of creating a custom adminhtml module, including admin routes,
controllers, layouts, blocks, grids, forms, menus, and ACL. By following the examples and guidelines provided, you
should be able to develop custom admin functionalities with ease.
