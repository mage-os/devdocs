# API Documentation: How to Use and Extend APIs in Magento 2

[TOC]

## Introduction

This documentation aims to provide you with a comprehensive guide on how to use and extend APIs in Magento 2. APIs (
Application Programming Interfaces) are fundamental tools for integrating and extending the functionality of Magento 2.
This document assumes a basic understanding of programming concepts and familiarity with PHP and Magento 2.

## API Basics

APIs in Magento 2 are built using a REST (Representational State Transfer) architecture. RESTful APIs allow you to
interact with Magento 2 resources, such as products, customers, orders, and more, by sending HTTP requests to specific
endpoints.

Magento 2 provides a set of pre-defined APIs that allow developers to perform various operations on the system. These
operations include reading, creating, updating, and deleting resources. However, you can also extend and customize these
APIs to suit your specific business needs.

## Using APIs in Magento 2

### Authentication

Before accessing the APIs, you need to authenticate your requests. Magento 2 supports both token-based and OAuth-based
authentication methods.

For token-based authentication, you need to generate a token for each user who wants to access the APIs. Tokens can be
generated through the Magento admin panel or programmatically via the API. Once you have a valid token, you can include
it in your requests using the `Authorization` header.

Here's an example using cURL:

```shell
curl -X GET -H "Authorization: Bearer YOUR_TOKEN" https://example.com/rest/V1/products
```

### Request Methods

Magento 2 APIs support the standard HTTP request methods: GET, POST, PUT, and DELETE. These methods correspond to
different operations:

- GET: Retrieve resources or collections.
- POST: Create new resources.
- PUT: Update existing resources.
- DELETE: Delete resources.

The choice of request method depends on the type of operation you want to perform. For example, if you want to retrieve
a list of products, you would use a GET request. If you want to create a new product, you would use a POST request.

### Data Formats

Magento 2 APIs support various data formats for both request payloads and responses. The most commonly used formats are
JSON (JavaScript Object Notation) and XML (eXtensible Markup Language).

By default, Magento 2 APIs return JSON responses. However, you can specify the desired response format by setting
the `Accept` header in your requests. For example, to request XML responses, you can include the following header:

```
Accept: application/xml
```

### API Endpoints

Magento 2 provides a wide range of pre-defined API endpoints for different resources. These endpoints follow a
consistent pattern:

```
https://example.com/rest/V1/{resource}/{id}
```

Where:

- `resource` is the name of the resource you want to interact with (e.g., `products`, `customers`, `orders`).
- `id` is an optional parameter specifying the identifier of a specific resource. If omitted, the endpoint returns a
  collection of resources.

Here are some examples of API endpoints:

```
GET https://example.com/rest/V1/products
GET https://example.com/rest/V1/products/10
POST https://example.com/rest/V1/products
PUT https://example.com/rest/V1/products/10
DELETE https://example.com/rest/V1/products/10
```

## Extending APIs in Magento 2

Magento 2 allows you to extend and customize the existing APIs to meet your specific business requirements. This section
covers three common techniques: creating custom API endpoints, adding custom methods to existing APIs, and modifying
existing API endpoints.

### Creating Custom API Endpoints

To create a custom API endpoint, you need to define a new route in a custom module. This route should map to a
controller that handles the API request and performs the desired actions.

Here's an example of how to create a custom API endpoint for retrieving a list of custom products:

1. Create a custom module (e.g., `Vendor_CustomApi`).
2. Define a new route in `etc/webapi.xml`:

```xml
<routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Webapi:etc/webapi.xsd">
    <route url="/V1/custom-products" method="GET" identity="Vendor_CustomApi::customProducts"/>
</routes>
```

3. Create a controller that handles the API request in `Controller/CustomProducts.php`:

```php
<?php

namespace Vendor\CustomApi\Controller;

use Magento\Framework\App\Action\HttpGetActionInterface;
use Magento\Framework\Controller\Result\JsonFactory;
use Magento\Framework\Webapi\Rest\Request;

class CustomProducts implements HttpGetActionInterface
{
    protected $resultJsonFactory;

    public function __construct(JsonFactory $resultJsonFactory)
    {
        $this->resultJsonFactory = $resultJsonFactory;
    }

    public function execute()
    {
        // Retrieve and return custom products
        $products = ... // Your custom logic here

        $result = $this->resultJsonFactory->create();
        return $result->setData($products);
    }
}
```

Now, you can access your custom API endpoint using the following URL:

```
GET https://example.com/rest/V1/custom-products
```

### Adding Custom Methods to Existing APIs

Magento 2 allows you to add custom methods to existing API interfaces without modifying the core code. This technique is
useful when you need to perform additional operations on a resource.

For example, let's say you want to add a custom method to the `Magento\Catalog\Api\ProductRepositoryInterface` to
retrieve a product by its SKU.

1. Create a custom module (e.g., `Vendor_CustomApi`).
2. Define a new interface that extends the existing API interface in `Api/ProductRepositoryInterface.php`:

```php
<?php

namespace Vendor\CustomApi\Api;

use Magento\Framework\Exception\NoSuchEntityException;

interface ProductRepositoryInterface extends \Magento\Catalog\Api\ProductRepositoryInterface
{
    /**
     * Retrieve a product by SKU.
     *
     * @param string $sku
     * @return \Magento\Catalog\Api\Data\ProductInterface
     * @throws NoSuchEntityException If the product does not exist.
     */
    public function getBySku($sku);
}
```

3. Create a custom implementation of the interface in `Model/ProductRepository.php`:

```php
<?php

namespace Vendor\CustomApi\Model;

use Magento\Catalog\Api\Data\ProductInterface;
use Magento\Catalog\Api\ProductRepositoryInterface;
use Magento\Framework\Exception\NoSuchEntityException;

class ProductRepository implements ProductRepositoryInterface
{
    protected $productRepository;

    public function __construct(ProductRepositoryInterface $productRepository)
    {
        $this->productRepository = $productRepository;
    }

    public function getBySku($sku)
    {
        // Implement your custom logic here

        return $this->productRepository->get($sku);
    }

    // Implement other methods from the original interface
}
```

4. Register your custom implementation in `di.xml`:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <preference for="Vendor\CustomApi\Api\ProductRepositoryInterface" type="Vendor\CustomApi\Model\ProductRepository"/>
</config>
```

Now, you can use the `getBySku` method in addition to the existing methods of the `ProductRepositoryInterface`.

### Modifying Existing API Endpoints

You might need to modify the behavior or response format of existing API endpoints provided by Magento 2. To do so, you
can use plugins or preferences to override the default behavior of the core classes.

For example, let's say you want to modify the response structure of the `/V1/products` endpoint to include additional
data.

1. Create a custom module (e.g., `Vendor_CustomApi`).
2. Create a plugin that intercepts the response of the `Magento\Catalog\Api\ProductRepositoryInterface::getList` method
   in `Plugin/ProductRepositoryPlugin.php`:

```php
<?php

namespace Vendor\CustomApi\Plugin;

use Magento\Catalog\Api\Data\ProductInterface;
use Magento\Catalog\Api\ProductRepositoryInterface;
use Magento\Framework\Api\SearchResultsInterface;
use Magento\Framework\Api\SearchResultsInterfaceFactory;

class ProductRepositoryPlugin
{
    protected $searchResultsFactory;

    public function __construct(SearchResultsInterfaceFactory $searchResultsFactory)
    {
        $this->searchResultsFactory = $searchResultsFactory;
    }

    public function afterGetList(
        ProductRepositoryInterface $subject,
        SearchResultsInterface $searchResults
    ): SearchResultsInterface {
        // Manipulate the search results or add additional data
        foreach ($searchResults->getItems() as $product) {
            if ($product instanceof ProductInterface) {
                // Add additional data to each product
                $product->setCustomData(...);
            }
        }

        return $searchResults;
    }
}
```

3. Register your plugin in `di.xml`:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Catalog\Api\ProductRepositoryInterface">
        <plugin name="vendor_customapi_product_repository_plugin" type="Vendor\CustomApi\Plugin\ProductRepositoryPlugin"
                sortOrder="1"/>
    </type>
</config>
```

Now, whenever the `/V1/products` endpoint is called, your plugin will intercept the response and modify it according to
your custom logic.

## Conclusion

APIs are powerful tools for integrating and extending the functionality of Magento 2. This documentation provided an
overview of using and extending APIs, covering topics such as authentication, request methods, data formats, API
endpoints, creating custom endpoints, adding custom methods, and modifying existing endpoints. By leveraging these
techniques, you can build robust and customized integrations with Magento 2.
