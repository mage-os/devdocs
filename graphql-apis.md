# GraphQL API Documentation

[TOC]

This document provides comprehensive documentation for the GraphQL APIs in Magento 2. It covers all the necessary
information to understand and utilize the APIs effectively.

## Introduction

GraphQL is a query language for APIs that provides a flexible and efficient alternative to traditional RESTful APIs.
Magento 2 provides a comprehensive GraphQL API that allows you to retrieve and manipulate data from the system. This
documentation will guide you through the process of utilizing the GraphQL APIs in Magento 2.

## Getting Started

To get started with the Magento 2 GraphQL API, you need to have a basic understanding of GraphQL and familiarity with
PHP and Magento 2. You'll also need to have a valid authentication token to access the API.

To authenticate and obtain an access token, you can use the Magento 2 token-based authentication system. Once you have
the token, you can include it in the headers of your GraphQL requests as follows:

```
Authorization: Bearer <access_token>
```

With the authentication in place, you can start using the GraphQL API to query and mutate data.

## Querying Data

To query data using the GraphQL API, you need to specify the fields you want to retrieve in your query. Here's an
example query to get a list of products:

```graphql
query {
  products {
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

In the above example, we are querying for a list of products and specifying the fields we want to
retrieve (`id`, `name`, `price`). Each field can have sub-fields, allowing you to traverse complex data structures.

## Mutating Data

In addition to querying data, you can also use the GraphQL API to mutate (create, update, or delete) data. Here's an
example mutation to create a new customer:

```graphql
mutation {
  createCustomer(input: {
    firstname: "John",
    lastname: "Doe",
    email: "john.doe@example.com",
    password: "password123"
  }) {
    customer {
      id
    }
  }
}
```

In the above example, we are using the `createCustomer` mutation to create a new customer. We provide the necessary
input fields (`firstname`, `lastname`, `email`, `password`) to create the customer. The response will include the newly
created customer's `id`.

## Paginating Results

When dealing with large result sets, it's important to paginate the results to improve performance. The GraphQL API
provides pagination capabilities using the `pageSize` and `currentPage` parameters. Here's an example of paginating
products:

```graphql
query {
  products(
    pageSize: 10,
    currentPage: 1
  ) {
    items {
      id
      name
    }
    total_count
  }
}
```

In the above example, we are querying for products and specifying the `pageSize` and `currentPage` parameters. These
parameters allow you to control the number of items per page and which page to retrieve.

## Filtering and Sorting

The GraphQL API allows you to filter and sort data based on specific criteria. You can use the `filter` parameter to
specify the filtering conditions and the `sort` parameter to define the sorting order. Here's an example of filtering
and sorting products:

```graphql
query {
  products(
    filter: {
      sku: {
        eq: "ABC123"
      }
    },
    sort: {
      name: ASC
    }
  ) {
    items {
      id
      name
    }
  }
}
```

In the above example, we are filtering products by the `sku` field and sorting them by the `name` field in ascending
order (`ASC`).

## Error Handling

When making GraphQL requests, it's important to handle errors properly. The GraphQL API returns detailed error messages
in case of any errors. Here's an example of an error response:

```json
{
    "errors": [
        {
            "message": "The requested SKU is not available.",
            "category": "graphql-authorization"
        }
    ]
}
```

In the above example, the error message indicates that the requested SKU is not available. The `category` field provides
additional information about the type of error.

## Authentication and Authorization

The Magento 2 GraphQL API supports authentication and authorization using access tokens. You can generate an access
token using the Magento 2 token-based authentication system. The access token should be included in the `Authorization`
header of your GraphQL requests.

To control access to specific resources, you can configure the GraphQL permissions in the Magento 2 admin panel. This
allows you to define which operations are allowed for different user roles.

## Caching

The GraphQL API in Magento 2 supports caching to improve performance. By default, GraphQL responses are cached based on
the query parameters and the user context. You can configure caching options in the Magento 2 admin panel.

## GraphQL Schema

The GraphQL API in Magento 2 follows a schema-driven approach. The schema defines the available types, queries,
mutations, and their respective fields. You can explore the GraphQL schema using tools like GraphiQL or GraphQL
Playground.

To retrieve the GraphQL schema, you can send a request to the following endpoint:

```
https://yourmagentoinstallation.com/graphql/schema?query={__schema{types{name}}}
```

In the above example, replace `yourmagentoinstallation.com` with your actual Magento 2 installation URL.

## Conclusion

This documentation provides a comprehensive guide to the GraphQL APIs in Magento 2. It covers the basics of querying and
mutating data, pagination, filtering and sorting, error handling, authentication and authorization, caching, and
exploring the GraphQL schema.

By utilizing the power of GraphQL, you can efficiently retrieve and manipulate data from your Magento 2 system,
providing a seamless and flexible experience for your users.
