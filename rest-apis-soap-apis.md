# REST APIs and SOAP APIs Documentation

[TOC]

## Introduction

This documentation provides an overview of REST APIs and SOAP APIs, their differences, and how to use them in the
context of PHP and Magento 2. Both REST and SOAP APIs are widely used in web development to facilitate communication
between different systems or applications.

## REST APIs

REST (Representational State Transfer) APIs are a popular architectural style for building web services. They utilize
the HTTP protocol and its methods (GET, POST, PUT, DELETE) to perform operations on resources. REST APIs are
lightweight, simple, and easier to understand and implement compared to SOAP.

### Using REST APIs in PHP and Magento 2

In PHP and Magento 2, you can use built-in libraries and frameworks, such as Guzzle, to work with REST APIs. Here's an
example of how to make a GET request to a REST API endpoint using Guzzle:

```php
use GuzzleHttp\Client;

$client = new Client();
$response = $client->get('https://api.example.com/users');

$body = $response->getBody();
$data = json_decode($body, true);
```

In the above code snippet, we create a `Client` instance from Guzzle and make a GET request to retrieve a list of users
from the API endpoint `https://api.example.com/users`. The response is then parsed as JSON and stored in the `$data`
variable.

### Example REST API Endpoint: Get User Information

To illustrate how to work with REST APIs further, let's consider an example endpoint that retrieves user information.

**Endpoint:** `/api/users/{id}`

**Method:** GET

**Parameters:**

- `id` (required): The ID of the user to retrieve information for.

**Response:**

```json
{
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com"
}
```

To retrieve user information using this REST API endpoint in PHP and Magento 2, you can modify the previous code snippet
as follows:

```php
$id = 123;
$response = $client->get('https://api.example.com/users/' . $id);
$body = $response->getBody();
$data = json_decode($body, true);

$userName = $data['name'];
$userEmail = $data['email'];
```

In the above code, we specify the user ID (123) and concatenate it with the API endpoint URL to retrieve information for
a specific user.

## SOAP APIs

SOAP (Simple Object Access Protocol) APIs are another way to build web services. They use XML to define their message
structure and typically operate over HTTP or other protocols. SOAP APIs are more complex and can offer advanced features
such as built-in error handling and security.

### Using SOAP APIs in PHP and Magento 2

To work with SOAP APIs in PHP and Magento 2, you can utilize the built-in `SoapClient` class. Here's an example of how
to call a SOAP API method:

```php
$wsdl = 'https://api.example.com/soap?wsdl';
$soapClient = new SoapClient($wsdl);

$response = $soapClient->getUserInfo(['id' => 123]);
$userInfo = $response->getUserInfoResult;
```

In the above code snippet, we create a `SoapClient` instance by providing the URL to the WSDL (Web Services Description
Language) file of the SOAP API. We then call the `getUserInfo` method, passing the required parameters as an associative
array. The response is stored in the `$userInfo` variable.

### Example SOAP API Method: Get User Information

Let's consider an example SOAP API method that retrieves user information.

**Method:** `getUserInfo`

**Parameters:**

- `id` (required): The ID of the user to retrieve information for.

**Response:**

```xml
<getUserInfoResponse>
    <getUserInfoResult>
        <id>123</id>
        <name>John Doe</name>
        <email>john.doe@example.com</email>
    </getUserInfoResult>
</getUserInfoResponse>
```

To call the `getUserInfo` SOAP API method in PHP and Magento 2, you can modify the previous code snippet as follows:

```php
$response = $soapClient->getUserInfo(['id' => 123]);
$userName = $response->getUserInfoResult->name;
$userEmail = $response->getUserInfoResult->email;
```

In the above code, we call the `getUserInfo` method, passing the user ID (123) as a parameter. The response is then
accessed using object notation to extract the user's name and email.

## Conclusion

In this documentation, we discussed the basics of REST APIs and SOAP APIs, their usage in PHP and Magento 2, and
provided examples of how to work with them. REST APIs are simpler and commonly used, while SOAP APIs offer advanced
features but have more complexity. By understanding these concepts and examples, you can effectively interact with REST
and SOAP APIs in your PHP and Magento 2 projects.
