# REST APIs Documentation

[TOC]

This documentation provides a comprehensive guide to using REST APIs in PHP and Magento 2. REST (Representational State
Transfer) APIs are a set of rules and conventions that enable communication between different software applications over
the internet. In this guide, we will cover the basics of REST APIs, how to make requests, handle responses, and provide
practical examples using PHP and Magento 2.

## 1. Introduction to REST APIs

REST APIs follow a client-server architecture, where the client (your application) makes requests to a server (the API)
to perform certain actions or retrieve information. REST APIs use standard HTTP methods such as GET, POST, PUT, and
DELETE to manipulate resources.

REST APIs in Magento 2 are organized around specific concepts, such as products, customers, orders, and categories. Each
of these concepts is represented by a resource, which can be accessed by a unique URL. For example, to retrieve
information about a product, you would make a GET request to the `/products/{productId}` endpoint.

## 2. Making API Requests

To make requests to REST APIs in PHP, you can use the cURL library, which provides a flexible and powerful set of
functions for making HTTP requests.

Here's an example of making a GET request to retrieve product information:

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://example.com/rest/V1/products/123');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);

// Process the response
if ($response) {
    $product = json_decode($response, true);
    // Handle the product data
} else {
    // Handle the error
}
```

In this example, we initialize a cURL handle (`$ch`), set the URL of the API endpoint, and enable
the `CURLOPT_RETURNTRANSFER` option to receive the response as a string. We then execute the request using `curl_exec()`
and close the cURL handle.

## 3. Handling API Responses

API responses typically come in the form of JSON (JavaScript Object Notation), which is a lightweight data interchange
format. JSON data can be easily parsed and manipulated using PHP's `json_decode()` function.

Here's an example of handling a response from the previous GET request:

```php
if ($response) {
    $product = json_decode($response, true);
    if ($product) {
        // Access specific product attributes
        $sku = $product['sku'];
        $name = $product['name'];
        $price = $product['price'];
        // Handle the retrieved product data
    } else {
        // Handle JSON decoding error
    }
} else {
    // Handle the error
}
```

In this example, we check if the response is not empty, then decode the JSON response into an associative array
using `json_decode()` with the `true` option. We can then access specific attributes of the product and perform the
necessary operations.

## 4. Authentication and Authorization

Magento 2 REST APIs require authentication and authorization to ensure secure access to resources. To authenticate, you
need to obtain an access token by sending a POST request with your credentials to the `/integration/admin/token`
endpoint.

Here's an example of obtaining an access token:

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://example.com/rest/V1/integration/admin/token');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
    'username' => 'admin',
    'password' => 'admin123'
]));
$response = curl_exec($ch);
curl_close($ch);

if ($response) {
    $token = json_decode($response, true);
    // Use the token for subsequent API requests
} else {
    // Handle the error
}
```

In this example, we send a POST request to the `/integration/admin/token` endpoint with the `username` and `password` as
JSON-encoded data in the request body. We then retrieve the access token from the response and use it for subsequent API
requests.

## 5. Practical Examples in PHP and Magento 2

To illustrate the usage of REST APIs in PHP and Magento 2, let's consider some practical examples.

### Example 1: Creating a New Product

To create a new product using the Magento 2 API, you would make a POST request to the `/products` endpoint with the
product data in the request body.

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://example.com/rest/V1/products');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
    'sku' => 'new-product',
    'name' => 'New Product',
    'price' => 9.99,
    // Additional product data
]));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer ' . $token,
    'Content-Type: application/json'
]);
$response = curl_exec($ch);
curl_close($ch);

if ($response) {
    // Handle the success response
} else {
    // Handle the error
}
```

In this example, we send a POST request to the `/products` endpoint with the product data included in the request body.
We also set the appropriate headers, including the access token obtained through authentication.

### Example 2: Retrieving Order Details

To retrieve details of a specific order using the Magento 2 API, you would make a GET request to the `/orders/{orderId}`
endpoint.

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://example.com/rest/V1/orders/123');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer ' . $token
]);
$response = curl_exec($ch);
curl_close($ch);

if ($response) {
    $order = json_decode($response, true);
    // Handle the retrieved order details
} else {
    // Handle the error
}
```

In this example, we send a GET request to the `/orders/{orderId}` endpoint, including the order ID in the URL. We also
include the access token in the request header for authentication.

### Example 3: Updating Customer Information

To update a customer's information using the Magento 2 API, you would make a PUT request to
the `/customers/{customerId}` endpoint with the updated data in the request body.

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://example.com/rest/V1/customers/123');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'PUT');
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
    'firstname' => 'John',
    'lastname' => 'Doe',
    // Additional customer data to update
]));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer ' . $token,
    'Content-Type: application/json'
]);
$response = curl_exec($ch);
curl_close($ch);

if ($response) {
    // Handle the success response
} else {
    // Handle the error
}
```

In this example, we send a PUT request to the `/customers/{customerId}` endpoint with the updated customer data in the
request body. We also set the appropriate headers, including the access token obtained through authentication.

## Conclusion

This documentation provided an overview of REST APIs, explained how to make requests, handle responses, and covered
authentication and authorization in PHP and Magento 2. We also provided practical examples to illustrate the concepts
discussed. With this knowledge, you should be able to confidently interact with REST APIs in your PHP and Magento 2
projects and leverage the power of remote resource manipulation.
