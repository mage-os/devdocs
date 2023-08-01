# Magento 2 Overview

[TOC]

This documentation provides an overview of Magento 2, a widely used and powerful e-commerce platform built on PHP.
Magento 2 offers a plethora of features, functionalities, and customization options to create robust and scalable online
stores. This guide will introduce you to the key components and concepts of Magento 2, providing you with a solid
foundation for further exploration.

## Architecture

Magento 2 follows a modular architecture that promotes flexibility and extensibility. The core functionality is divided
into various modules that can be enabled or disabled as per the requirements of your online store. Additionally, custom
modules can be developed to extend or modify the existing functionality. Let's take a look at the key architectural
components:

### Modules

Modules are the building blocks of Magento 2. Each module encapsulates a specific functionality, such as catalog
management, checkout, customer management, etc. They define the structure, behavior, and available APIs of their
respective domains. Modules can depend on other modules, creating a modular and flexible system. You can develop your
own modules or leverage existing ones from the Magento Marketplace.

### Themes

Themes define the visual appearance of your Magento 2 store. A theme includes various components like templates,
layouts, CSS, and JavaScript files. Magento 2 provides a default theme, but you can customize it or create your own
theme to suit your brand and requirements. Customizing the theme allows you to create a unique and personalized shopping
experience for your customers.

## Key Concepts

To effectively work with Magento 2, it's crucial to understand the key concepts that underpin its architecture and
functionality. Let's explore some of these concepts:

### Stores, Websites, and Store Views

A Magento 2 installation can have multiple stores, each representing a separate website or brand. Each store can have
multiple websites, and each website can have multiple store views. Store views define different languages, currencies,
and other localized settings. This hierarchical structure allows you to manage multiple online stores from a single
Magento 2 installation.

### Entity-Attribute-Value (EAV) Database Model

The EAV database model is employed by Magento 2 to store and manage a wide range of data. It allows for flexible and
scalable data storage by providing a dynamic way to add attributes to entities. For example, the product catalog uses
the EAV model to store product attributes like name, SKU, price, etc. Understanding the EAV model helps in effectively
querying and manipulating data in Magento 2.

### Dependency Injection (DI)

Magento 2 extensively utilizes the concept of dependency injection to manage object dependencies. Dependency injection
allows for loose coupling, easier testing, and better maintainability of code. The DI mechanism in Magento 2 relies on
XML configuration files and constructor injection. Here's an example of constructor injection in a custom module:

```php
namespace Vendor\Module\Model;

use Magento\Framework\App\Config\ScopeConfigInterface;

class MyModel
{
    private $scopeConfig;

    public function __construct(ScopeConfigInterface $scopeConfig)
    {
        $this->scopeConfig = $scopeConfig;
    }

    // ...
}
```

### Service Contracts

Service contracts define a set of API interfaces that expose the functionality of a module. They provide a standardized
way to interact with the underlying business logic without directly accessing the implementation details. Service
contracts enhance the stability and compatibility of Magento 2, allowing for easy upgrades and third-party integrations.
For example, the `ProductRepositoryInterface` provides methods to create, read, update, and delete products.

```php
namespace Magento\Catalog\Api;

use Magento\Catalog\Api\Data\ProductInterface;

interface ProductRepositoryInterface
{
    public function save(ProductInterface $product);
    public function getById($id);
    // ...
}
```

## Conclusion

This overview provides you with a glimpse into the architecture and key concepts of Magento 2. Understanding these
components and concepts is essential for building and customizing online stores on the Magento 2 platform. You can now
delve deeper into each topic and explore the vast capabilities that Magento 2 offers for e-commerce development. Happy
coding!
