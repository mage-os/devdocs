# Web API Documentation

[TOC]

## Introduction

Welcome to the Web API documentation for Magento 2! This document aims to provide you with all the necessary information
to interact with Magento's Web API using PHP.

Magento's Web API allows you to programmatically interact with various resources and perform CRUD (Create, Read, Update,
Delete) operations on them. It provides a secure and standardized way to access and manipulate data within a Magento
installation.

## Authentication

Before you can start using the Web API, you need to authenticate your requests. Magento 2 supports token-based
authentication using OAuth. To obtain an access token, you need to follow these steps:

1. Create an integration in your Magento admin panel. Go to *System* > *Extensions* > *Integrations* and click on *Add
   New Integration*.

2. Fill in the integration details and assign the appropriate permissions to the integration.

3. Once you have created the integration, Magento will generate a set of consumer key and consumer secret.

4. To obtain an access token, you need to make a POST request to the `/V1/integration/admin/token` endpoint with the
   consumer key and secret as the payload. Here's an example using cURL:

```bash
curl -X POST \
  'https://your-magento-installation.com/rest/V1/integration/admin/token' \
  -H 'Content-Type: application/json' \
  -d '{
    "username": "your-username",
    "password": "your-password"
  }'
```

5. The response will be the access token that you can use to authenticate subsequent requests. Make sure to securely
   store and handle this token.

## API Endpoints

Magento's Web API provides a wide range of endpoints to interact with various resources such as customers, products,
orders, and more. Each endpoint follows a consistent URL structure:

```
https://your-magento-installation.com/rest/<version>/<resource>
```

For example, to get a list of all customers, you would make a GET request to `/V1/customers`. Similarly, to create a new
product, you would make a POST request to `/V1/products`.

## Request and Response Format

All requests to the Web API should be made using the HTTP protocol, with appropriate HTTP methods such as GET, POST,
PUT, and DELETE, depending on the operation you want to perform.

The request payloads and response bodies are typically in JSON format. Make sure to set the `Content-Type` header
to `application/json` for requests that have a payload.

Here's an example of a request to create a new product:

```php
<?php

$accessToken = 'your-access-token';
$endpoint = 'https://your-magento-installation.com/rest/V1/products';

$data = [
    'product' => [
        'sku' => 'test-product',
        'name' => 'Test Product',
        'price' => 10,
        'status' => 1
        // ... other product attributes
    ]
];

$ch = curl_init($endpoint);

curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
    'Authorization: Bearer ' . $accessToken
]);

$response = curl_exec($ch);

curl_close($ch);

// Handle the response as needed
```

## Error Handling

When interacting with the Web API, it's important to handle errors gracefully. If a request fails, the response will
include an appropriate HTTP status code along with an error message in the response body.

For example, if you make a request to create a new product without providing required attributes, you will receive
a `400 Bad Request` response with an error message indicating the missing attributes.

Make sure to check the HTTP status code and the response body to handle errors appropriately in your code.

## Conclusion

Congratulations! You now have a solid understanding of Magento 2's Web API and how to interact with it using PHP. You
should be able to make requests to various endpoints, authenticate using OAuth, handle errors, and perform CRUD
operations on different resources.

For more detailed information on specific endpoints and available operations, refer to the official Magento 2 Web API
documentation.

Happy coding!
