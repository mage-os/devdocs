# Module Development Documentation

[TOC]

## Introduction

This documentation serves as a guide for module development in Magento 2, specifically focusing on PHP-based module
development. It assumes that you have a working knowledge of PHP and familiarity with Magento 2's architecture and
concepts.

## Module Structure

A Magento 2 module is organized in the following directory structure:

```
app
└── code
    └── Vendor
        └── Module
            ├── etc
            │   ├── module.xml
            │   └── other_configuration_files.xml
            ├── Model
            │   ├── ResourceModel
            │   └── other_model_classes.php
            ├── Controller
            │   └── other_controller_classes.php
            ├── Block
            │   └── other_block_classes.php
            ├── view
            │   ├── frontend
            │   └── adminhtml
            └── other_files_and_directories
```

Here, `Vendor` refers to your company or organization name, and `Module` is the name of your module. You should replace
these placeholders with appropriate names.

The `etc` directory contains module configuration files, such as `module.xml` that defines the module's identity.

The `Model` directory contains model classes and resource models, while the `Controller` directory holds controller
classes for handling requests.

The `Block` directory contains block classes responsible for rendering templates.

The `view` directory houses frontend and adminhtml directories, which contain layout XML files, templates, and other
view-related files.

## Module Registration

To register your module with Magento 2, you need to create a `module.xml` file in your module's `etc` directory. Here's
an example `module.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Vendor_Module">
        <sequence>
            <module name="Magento_Cms"/>
        </sequence>
    </module>
</config>
```

In this example, `Vendor_Module` is the module's name. The `<sequence>` tag defines any
modules that your module depends on. In this case, it depends on `Magento_Cms`.

## Module Configuration

To add configuration settings for your module, create a configuration XML file in your module's `etc` directory. For
example, if your module is named `Vendor_Module`, create a file named `module_config.xml`.

Here's an example of a `module_config.xml` file:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Store:etc/config.xsd">
    <default>
        <vendor_module>
            <general>
                <enabled>1</enabled>
                <some_other_setting>value</some_other_setting>
            </general>
        </vendor_module>
    </default>
</config>
```

In this example, the module's configuration settings are placed under the `<vendor_module>` tag. You can define any
number of settings within the `<general>` tag.

To access these settings in your module code, you can use the following code snippet:

```php
$isEnabled = $this->scopeConfig->getValue('vendor_module/general/enabled');
```

Here, `$this->scopeConfig` is an instance of `\Magento\Framework\App\Config\ScopeConfigInterface`.

## Event Observers

Magento 2 provides an event-driven architecture, allowing modules to observe and react to specific events that occur
during the application's execution. To create an event observer in your module, follow these steps:

1. Create an XML file named `events.xml` in your module's `etc` directory.
2. Define your event observer inside this file. Here's an example:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="checkout_onepage_controller_success_action">
        <observer name="vendor_module_checkout_success" instance="Vendor\Module\Observer\CheckoutSuccessObserver"/>
    </event>
</config>
```

In this example, we're observing the `checkout_onepage_controller_success_action` event and linking it to
the `Vendor\Module\Observer\CheckoutSuccessObserver` class.

3. Implement the observer class with the necessary logic. Here's an example:

```php
<?php
namespace Vendor\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class CheckoutSuccessObserver implements ObserverInterface
{
    public function execute(Observer $observer)
    {
        // Your logic here
    }
}
```

Remember to replace `Vendor\Module` with your module's namespace.

## Custom Controllers

To create a custom controller in your module, follow these steps:

1. Create a PHP class file for your controller, e.g., `CustomController.php`.
2. Implement the necessary logic inside the class. Here's an example:

```php
<?php
namespace Vendor\Module\Controller\Custom;

use Magento\Framework\App\Action\Action;
use Magento\Framework\App\Action\Context;
use Magento\Framework\View\Result\PageFactory;

class CustomController extends Action
{
    protected $resultPageFactory;

    public function __construct(Context $context, PageFactory $resultPageFactory)
    {
        parent::__construct($context);
        $this->resultPageFactory = $resultPageFactory;
    }

    public function execute()
    {
        $resultPage = $this->resultPageFactory->create();
        return $resultPage;
    }
}
```

In this example, the `execute()` method returns a `Page` result, which can be used to render a page template.

3. Register your controller in your module's `routes.xml` file. Here's an example:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route id="vendor_module" frontName="custom">
            <module name="Vendor_Module"/>
        </route>
    </router>
</config>
```

In this example, we're registering the `Vendor\Module\Controller\Custom\CustomController` under the route `custom`.

## Block and Template Files

Blocks are responsible for providing data to templates and rendering them in Magento 2. To create a block and template
file, follow these steps:

1. Create a PHP class file for your block, e.g., `CustomBlock.php`.
2. Implement the necessary logic inside the class. Here's an example:

```php
<?php
namespace Vendor\Module\Block;

use Magento\Framework\View\Element\Template;

class CustomBlock extends Template
{
    public function getCustomData()
    {
        return "Custom data from the block.";
    }
}
```

3. Create a template file, e.g., `custom_template.phtml`. Here's an example:

```html
<h1><?php echo $block->getCustomData(); ?></h1>
```

In this example, `$block` refers to an instance of `CustomBlock`.

4. Use your block and template in a layout XML file. Here's an example:

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Vendor\Module\Block\CustomBlock" name="custom.block"
                   template="Vendor_Module::custom_template.phtml"/>
        </referenceContainer>
    </body>
</page>
```

In this example, we're adding the `custom.block` block to the `content` container and using the `custom_template.phtml`
template.

## Database Setup

Magento 2 uses Declarative schema setup to create and modify database tables and perform other setup tasks. To create a
declarative schema script, follow these steps:

1. Create a file named `db_schema.xml` inside your module's `etc` directory.
2. Implement the necessary logic inside the file. Here's an example:

```xml
<table name="custom_table" resource="default" engine="innodb"
           comment="Custom Table">
    <column xsi:type="int" name="entity_id" unsigned="false" nullable="false" identity="true" comment="Entity ID"/>
    <column xsi:type="varchar" name="name" nullable="false" length="255" default="" comment="name"/>
    <column xsi:type="timestamp" name="created_at" on_update="false" nullable="false" default="CURRENT_TIMESTAMP" comment="Created At"/>
    <constraint xsi:type="primary" referenceId="PRIMARY">
        <column name="entity_id"/>
    </constraint>
</table>
```

In this example, we're creating a table named `custom_table` with three columns: `entity_id`, `name`, and `created_at`.

3. Run the whitelist generation command:

```
bin/magento setup:db-declaration:generate-whitelist --module-name=Vendor_Module
```
4. Run the setup upgrade command to apply your schema changes:

```shell
bin/magento setup:upgrade
```

## API Integration

Magento 2 provides a robust framework for building and integrating APIs. To create a custom API endpoint in your module,
follow these steps:

1. Create a PHP class file for your API endpoint, e.g., `CustomApi.php`.
2. Implement the necessary logic inside the class. Here's an example:

```php
<?php
namespace Vendor\Module\Api;

interface CustomApiInterface
{
    /**
     * @param mixed $id
     * @return string
     */
    public function getById($id);
}
```

3. Create a PHP class file for your API implementation, e.g., `CustomApiImpl.php`.
4. Implement the necessary logic inside the class. Here's an example:

```php
<?php
namespace Vendor\Module\Api;

class CustomApiImpl implements CustomApiInterface
{
    /**
     * @param mixed $id
     * @return string
     */
    public function getById($id)
    {
        // Your logic here
    }
}
```

5. Register your API endpoint in `etc/webapi.xml`. Here's an example:

```xml
<?xml version="1.0"?>
<routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Webapi:etc/webapi.xsd">
    <route url="/V1/custom/:id" method="GET">
        <service class="Vendor\Module\Api\CustomApiInterface" method="getById"/>
        <resources>
            <resource ref="anonymous"/>
        </resources>
    </route>
</routes>
```

In this example, we're defining a route for the `GET` HTTP method, with the URL pattern `/V1/custom/:id`. The `class`
attribute refers to your API implementation class, and the `method` attribute specifies the method to be called.

## Custom GraphQL Types

Magento 2 supports GraphQL, a modern API query language. To create a custom GraphQL type in your module, follow these
steps:

1. Create a PHP class file for your custom GraphQL type, e.g., `CustomType.php`.
2. Implement the necessary logic inside the class. Here's an example:

```php
<?php
namespace Vendor\Module\Model\Resolver;

use Magento\Framework\GraphQl\Config\Element\Field;
use Magento\Framework\GraphQl\Query\ResolverInterface;
use Magento\Framework\GraphQl\Schema\Type\ResolveInfo;

class CustomType implements ResolverInterface
{
    public function resolve(Field $field, $context, ResolveInfo $info, array $value = null, array $args = null)
    {
        // Your logic here
    }
}
```

3. Register your custom GraphQL type in `etc/schema.graphqls`. Here's an example:

```graphql
type Query {
    customData: CustomType @resolver(class: "Vendor\\Module\\Model\\Resolver\\CustomType")
}
```

In this example, we're defining a query field `customData` of type `CustomType`, resolved by
the `Vendor\Module\Model\Resolver\CustomType` class.

## Testing and Quality Assurance

Magento 2 provides a testing framework for module testing and quality assurance. To create tests for your module, follow
these steps:

1. Create a `Test` directory inside your module directory.
2. Create a PHP test class file, e.g., `CustomTest.php`, inside the `Test` directory.
3. Implement your tests inside the class using PHPUnit. Here's an example:

```php
<?php
namespace Vendor\Module\Test;

use Magento\Framework\TestFramework\Unit\Helper\ObjectManager;
use PHPUnit\Framework\TestCase;

class CustomTest extends TestCase
{
    protected function setUp(): void
    {
        $objectManager = new ObjectManager($this);
        // Initialize necessary dependencies
    }

    public function testSomething()
    {
        // Your test logic here
    }
}
```

In this example, we're using the Magento 2 `ObjectManager` to initialize necessary dependencies for testing.

4. Run your tests using the following command:

```shell
bin/magento dev:tests:run unit --testsuite=Vendor_Module
```

Replace `Vendor_Module` with your module's test suite identifier.

## Conclusion

This documentation provides a comprehensive overview of module development in Magento 2. We covered various aspects such
as module structure, registration, configuration, event observers, custom controllers, block and template files,
database setup, API integration, custom GraphQL types, and testing.

By following these guidelines and examples, you should be able to develop robust and maintainable modules that integrate
seamlessly with Magento 2. Happy coding!
