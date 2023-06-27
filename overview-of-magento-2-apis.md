# Magento 2 API Overview

- [Magento 2 API Overview](#magento-2-api-overview)
    * [REST and SOAP APIs](#rest-and-soap-apis)
    * [Endpoints](#endpoints)
    * [Authentication](#authentication)
    * [Usage Limits](#usage-limits)
    * [Asynchronous API](#asynchronous-api)
    * [GraphQL](#graphql)

Magento 2 APIs, commonly referred to as web APIs, allow third-party services to integrate with Magento using REST (
Representational State Transfer) and SOAP (Simple Object Access Protocol). These APIs ensure that data can be seamlessly
passed between Magento and other systems, such as ERP systems, CRM platforms, mobile apps, and more.

## REST and SOAP APIs

REST and SOAP are two different approaches to network communication in web services. REST APIs use HTTP methods to
retrieve and send data and are typically easier to work with. SOAP, on the other hand, is a protocol with a defined
standard to communicate, providing a robust and extensible option.

## Endpoints

Magento 2 provides numerous API endpoints, segregated by modules such as customers, products, orders, and more. Each
endpoint corresponds to a specific type of resource.

## Authentication

Magento 2 supports both token-based authentication and OAuth-based authentication, depending on the level of access and
type of integration.

## Usage Limits

While Magento 2 Open Source does not impose any specific usage limits on its APIs, your server or hosting provider
might. Magento 2 Commerce can be configured to enforce customizable API rate limiting.

## Asynchronous API

To optimize performance and user experience, Magento 2.3 introduced Asynchronous API. This enables requests to be
processed in the background, freeing up the server to handle other requests.

## GraphQL

Starting from Magento 2.3, Magento also supports GraphQL, an open-source data query and manipulation language for APIs,
providing a more efficient alternative to traditional REST/SOAP.
