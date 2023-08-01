# Magento 2 Development Overview

[TOC]

## Introduction

Welcome to the overview of Magento 2 development! In this document, we will provide you with a comprehensive
understanding of the key concepts, tools, and techniques involved in developing with Magento 2. Whether you are a
seasoned Magento developer or new to the platform, this documentation will serve as a valuable resource to further
enhance your skills and knowledge.

## Architecture <a name="architecture"></a>

Magento 2 follows a modular architecture that allows for easy customization and extension. The core functionality is
divided into separate modules, which can be customized or extended as per your business requirements. The modular
structure also promotes code reusability and maintainability.

## Modules <a name="modules"></a>

Modules are the building blocks of Magento 2. They encapsulate specific functionalities and can be easily added,
removed, or disabled. A module consists of various components such as controllers, models, blocks, and templates.

To create a custom module, you need to define its structure in the `app/code` directory. Let's take an example of a
module named `MyCompany_MyModule`.

```markdown
app/
code/
MyCompany/
MyModule/
etc/
module.xml
registration.php
```

The `module.xml` file defines the module's configuration, while `registration.php` registers the module with Magento.

## Themes <a name="themes"></a>

Themes in Magento 2 control the visual appearance of your store. They consist of various components such as layouts,
templates, CSS, and JavaScript files. You can create a custom theme to give your store a unique look and feel.

To create a custom theme, define its structure in the `app/design` directory. For example, to create a theme
named `MyCompany/mytheme`, the directory structure would be as follows:

```markdown
app/
design/
frontend/
MyCompany/
mytheme/
etc/
view.xml
registration.php
```

The `view.xml` file allows you to configure various aspects of the theme, such as image sizes, widgets, and responsive
behavior.

## Layouts <a name="layouts"></a>

Layouts in Magento 2 define the structure and composition of the pages. They are XML files that specify the arrangement
of blocks and containers on a page. Layout files are located in the `app/design` directory.

Here's an example of a layout file named `catalog_product_view.xml`:

```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceBlock name="product.info.stock.sku" remove="true"/>
        <move element="product.info.review" destination="product.info.main" before="-"/>
    </body>
</page>
```

In this example, we remove the SKU block from the product page and move the review block before all other blocks within
the `product.info.main` container.

## Blocks <a name="blocks"></a>

Blocks in Magento 2 encapsulate reusable components that provide specific functionalities. They are PHP classes
responsible for handling business logic and generating HTML output. Blocks can be referenced and manipulated within
layout XML files.

Here's an example of a block class named `MyCompany\MyModule\Block\Product\View`:

```php
<?php

namespace MyCompany\MyModule\Block\Product;

use Magento\Framework\View\Element\Template;

class View extends Template
{
    public function getProduct()
    {
        return $this->_coreRegistry->registry('current_product');
    }
}
```

In this example, the block extends the `Template` class and provides a method to retrieve the current product from the
registry.

## Models <a name="models"></a>

Models in Magento 2 represent the business entities and handle data manipulation. They interact with the database and
provide an interface for retrieving, creating, updating, and deleting records.

Here's an example of a model class named `MyCompany\MyModule\Model\Product`:

```php
<?php

namespace MyCompany\MyModule\Model;

use Magento\Framework\Model\AbstractModel;

class Product extends AbstractModel
{
    protected function _construct()
    {
        $this->_init(\MyCompany\MyModule\Model\ResourceModel\Product::class);
    }
}
```

In this example, the model extends the `AbstractModel` class and initializes the resource model.

## Controllers <a name="controllers"></a>

Controllers in Magento 2 handle incoming HTTP requests and generate responses. They are responsible for executing the
requested action and rendering the appropriate view. Controllers can be extended or overridden to modify the default
behavior.

Here's an example of a controller class named `MyCompany\MyModule\Controller\Product\View`:

```php
<?php

namespace MyCompany\MyModule\Controller\Product;

use Magento\Framework\App\Action\Action;
use Magento\Framework\App\Action\Context;
use Magento\Framework\View\Result\PageFactory;

class View extends Action
{
    protected $resultPageFactory;

    public function __construct(Context $context, PageFactory $resultPageFactory)
    {
        parent::__construct($context);
        $this->resultPageFactory = $resultPageFactory;
    }

    public function execute()
    {
        return $this->resultPageFactory->create();
    }
}
```

In this example, the controller extends the `Action` class and uses the `PageFactory` to generate a result page.

## Events and Observers <a name="events-and-observers"></a>

Events and observers in Magento 2 provide a way to extend or modify the default behavior without modifying the core
code. Events are dispatched at specific points in the code, and observers listen for these events and execute custom
logic.

Here's an example of an event dispatch in Magento 2:

```php
<?php

namespace MyCompany\MyModule\Controller\Product;

use Magento\Framework\Event\ManagerInterface;

class View extends \Magento\Framework\App\Action\Action
{
    protected $eventManager;

    public function __construct(Context $context, ManagerInterface $eventManager)
    {
        parent::__construct($context);
        $this->eventManager = $eventManager;
    }

    public function execute()
    {
        // Dispatch the event
        $this->eventManager->dispatch('my_module_product_view', ['product' => $product]);
    }
}
```

An observer can then listen to this event and perform custom actions. For example:

```php
<?php

namespace MyCompany\MyModule\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class ProductView implements ObserverInterface
{
    public function execute(Observer $observer)
    {
        $product = $observer->getData('product');
        // Perform custom logic
    }
}
```

## Plugins <a name="plugins"></a>

Plugins in Magento 2 provide a way to modify or extend the behavior of public class methods. They allow you to intercept
method calls and perform custom actions before, after, or around the original method execution.

Here's an example of a plugin class:

```php
<?php

namespace MyCompany\MyModule\Plugin;

class MyPlugin
{
    public function beforeSomeMethod($subject, $arg1, $arg2)
    {
        // Perform actions before the original method
        return [$arg1, $arg2];
    }

    public function afterSomeMethod($subject, $result)
    {
        // Perform actions after the original method
        return $result;
    }

    public function aroundSomeMethod($subject, callable $proceed, $arg1, $arg2)
    {
        // Perform actions before the original method
        $result = $proceed($arg1, $arg2);
        // Perform actions after the original method
        return $result;
    }
}
```

In this example, the `beforeSomeMethod()` method is called before the original method, `afterSomeMethod()` is called
after the original method, and `aroundSomeMethod()` is called both before and after the original method.

## Web APIs <a name="web-apis"></a>

Magento 2 provides a comprehensive set of web APIs that allow external systems to interact with the platform. Web APIs
enable you to create, read, update, and delete data using standard HTTP methods.

To use web APIs, you need to define your API endpoints and specify the required authentication and permissions. Magento
provides a range of authentication methods such as OAuth, token-based, and guest access.

For example, to create a custom API endpoint to retrieve product information, you would define the endpoint in a
module's `etc/webapi.xml` file and implement the corresponding interface and class.

## Testing <a name="testing"></a>

Magento 2 emphasizes the importance of testing by providing a robust testing framework. The framework includes unit
tests, integration tests, and functional tests. Writing tests for your custom modules and themes helps ensure the
stability and reliability of your codebase.

Magento 2 uses PHPUnit as the testing framework. You can write tests for your modules in the `Test/Unit` directory and
execute them using the command-line interface.

## Conclusion

This overview of Magento 2 development has provided you with a solid foundation to delve deeper into the various aspects
of Magento 2. Armed with this knowledge, you are now equipped to create custom modules, themes, and extensions, and
harness the power of Magento 2 to build scalable and robust e-commerce solutions. Happy coding!
