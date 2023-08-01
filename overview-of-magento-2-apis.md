# Magento 2 APIs Overview

[TOC]

## Introduction

Magento 2 is a powerful ecommerce platform that provides a wide range of APIs for developers to build and extend their
online stores. These APIs enable developers to interact with various components of the Magento system, such as products,
customers, orders, and more. In this documentation, we will provide an overview of the different types of APIs available
in Magento 2 and how to use them effectively.

## Types of APIs in Magento 2

Magento 2 offers three main types of APIs:

1. **Web APIs**: These APIs allow remote systems to interact with the Magento 2 platform using HTTP(S) protocols. Web
   APIs are based on Representational State Transfer (REST) and support both JSON and XML data formats. They provide
   CRUD operations (Create, Read, Update, Delete) for various entities in the Magento system. Web APIs are ideal for
   building integrations with third-party systems, mobile apps, or custom frontend applications.

2. **Service Contracts**: Service Contracts are PHP interfaces that define the public API of a module. They provide a
   more structured and reliable way to interact with Magento 2 modules compared to direct database operations or custom
   SQL queries. Service Contracts enforce a separation of concerns between the module’s business logic and its data
   storage and retrieval. They are mainly used by other modules within the Magento system.

3. **GraphQL APIs**: GraphQL is an alternative to REST for querying and manipulating data. It provides a flexible and
   efficient way to request only the specific data needed, reducing the amount of data sent over the wire. GraphQL APIs
   in Magento 2 are built on top of the underlying Service Contracts and provide a powerful tool for frontend developers
   to retrieve data from the Magento system.

## Web APIs

Magento 2 Web APIs provide a comprehensive set of endpoints for interacting with different entities, including products,
customers, orders, categories, and more. Each entity has its own set of API endpoints that follow a consistent URL
structure. For example, to retrieve a list of products, you would use the `/V1/products` endpoint.

Web APIs are authenticated using the OAuth 1.0a protocol or token-based authentication. OAuth 1.0a provides a secure
mechanism for authenticating external systems with the Magento platform. Token-based authentication, on the other hand,
is simpler to implement and doesn't require the complex OAuth flow.

Here's an example of how to retrieve a list of products using a token-based authentication:

```php
$token = 'your_token_here';
$baseUrl = 'https://your_magento_store.com/rest/V1';

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $baseUrl . '/products');
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer ' . $token,
    'Content-Type: application/json'
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

$result = json_decode($response, true);
```

## Service Contracts

Service Contracts in Magento 2 provide a standardized way to interact with module functionality. They define a set of
PHP interfaces that represent the public API of a module. By adhering to these interfaces, developers ensure that their
code is compatible with future versions of Magento and other third-party modules.

For example, to create a new customer using Service Contracts, you would use the `CustomerRepositoryInterface`:

```php
use Magento\Customer\Api\CustomerRepositoryInterface;
use Magento\Customer\Api\Data\CustomerInterfaceFactory;

class CustomerCreator
{
    private $customerRepository;
    private $customerFactory;

    public function __construct(
        CustomerRepositoryInterface $customerRepository,
        CustomerInterfaceFactory $customerFactory
    ) {
        $this->customerRepository = $customerRepository;
        $this->customerFactory = $customerFactory;
    }

    public function createCustomer($data)
    {
        $customer = $this->customerFactory->create();
        // Set customer data

        $customer = $this->customerRepository->save($customer);
        return $customer;
    }
}
```

## GraphQL APIs

Magento 2's GraphQL APIs provide a flexible and efficient way to retrieve and manipulate data. With GraphQL, frontend
developers can request only the specific data they need, reducing the number of requests and the amount of data
transferred between the server and client.

To retrieve a list of products using GraphQL, you would write a query like this:

```graphql
{
  products(search: "t-shirt") {
    items {
      id
      name
      price {
        regularPrice {
          amount {
            value
            currency
          }
        }
      }
    }
  }
}
```

This query will return a list of products matching the search term "t-shirt" along with their names and prices.

## Conclusion

Magento 2 provides a powerful set of APIs that enable developers to build and extend their online stores. Web APIs,
Service Contracts, and GraphQL APIs offer different ways to interact with the Magento system, depending on the use case
and requirements of your project. By leveraging these APIs effectively, you can create custom integrations, build mobile
apps, and enhance the functionality of your Magento 2 store.
