# Overview of Architectural Components

[TOC]

This documentation provides an overview of the architectural components used in PHP and Magento 2 development.
Understanding these components is crucial for building robust and scalable applications. We will discuss the key
architectural components and their roles in the software development process.

## Model-View-Controller (MVC) Pattern

The Model-View-Controller (MVC) pattern is a widely adopted architectural pattern for designing web applications. It
separates the application into three interconnected components: Model, View, and Controller.

### Model

The Model represents the data and business logic of the application. It is responsible for handling data storage,
retrieval, and manipulation. In Magento 2, Models are typically implemented as PHP classes that interact with the
database.

Example:

```php
namespace Vendor\Module\Model;

use Magento\Framework\Model\AbstractModel;

class Product extends AbstractModel
{
    protected function _construct()
    {
        $this->_init(\Vendor\Module\Model\ResourceModel\Product::class);
    }
    
    // Model methods
}
```

### View

The View is responsible for presenting the data to the user. It generates the HTML output and handles user interactions.
In Magento 2, Views are implemented using XML and PHTML templates.

Example (XML layout file):

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Vendor\Module\Block\Product" name="product_view"
                   template="Vendor_Module::product/view.phtml"/>
        </referenceContainer>
    </body>
</page>
```

### Controller

The Controller receives user requests, processes them, and interacts with the Model and View components. It is
responsible for handling business logic, such as validating input, executing actions, and returning responses. In
Magento 2, Controllers are implemented as PHP classes.

Example:

```php
namespace Vendor\Module\Controller\Product;

use Magento\Framework\App\Action\Action;
use Magento\Framework\App\Action\Context;
use Vendor\Module\Model\ProductFactory;

class View extends Action
{
    protected $productFactory;
    
    public function __construct(Context $context, ProductFactory $productFactory)
    {
        parent::__construct($context);
        $this->productFactory = $productFactory;
    }
    
    public function execute()
    {
        $productId = $this->getRequest()->getParam('id');
        $product = $this->productFactory->create()->load($productId);
        
        // Process and pass data to the View
        
        return $this->resultFactory->create(\Magento\Framework\Controller\ResultFactory::TYPE_PAGE);
    }
}
```

## Service Contracts

Service Contracts provide a standardized interface for interacting with system components. They define a set of methods
that can be called by other components, ensuring consistency and flexibility in the system architecture. Magento 2
extensively uses Service Contracts to decouple modules and facilitate interoperability.

Example (Service Contract interface):

```php
namespace Vendor\Module\Api;

interface ProductServiceInterface
{
    /**
     * Get product by ID
     *
     * @param int $productId
     * @return \Vendor\Module\Api\Data\ProductInterface
     * @throws \Magento\Framework\Exception\NoSuchEntityException
     */
    public function getProduct($productId);
    
    // Other methods
}
```

## Dependency Injection (DI)

Dependency Injection (DI) is a design pattern used to manage component dependencies and improve code maintainability and
testability. In Magento 2, DI is implemented using configuration files and annotations. It allows components to request
dependencies from a centralized container, reducing coupling and enabling module customization.

Example (DI configuration file):

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <preference for="Vendor\Module\Api\ProductServiceInterface" type="Vendor\Module\Model\ProductService"/>
</config>
```

Example (DI annotation):

```php
namespace Vendor\Module\Model;

use Vendor\Module\Api\ProductServiceInterface;

class ProductService implements ProductServiceInterface
{
    /**
     * @var \Vendor\Module\Model\ProductFactory
     */
    protected $productFactory;
    
    /**
     * @param \Vendor\Module\Model\ProductFactory $productFactory
     */
    public function __construct(ProductFactory $productFactory)
    {
        $this->productFactory = $productFactory;
    }
    
    // Implement interface methods
}
```

## Conclusion

Understanding the architectural components used in PHP and Magento 2 development is crucial for building scalable and
maintainable applications. The Model-View-Controller (MVC) pattern provides a clear separation of concerns, while
Service Contracts and Dependency Injection (DI) enable modular and customizable development. By leveraging these
architectural components, developers can create robust and flexible applications that meet the needs of their clients or
businesses.
