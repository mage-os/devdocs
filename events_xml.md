# `events.xml` Reference Documentation

[TOC]

The `events.xml` file in Magento 2 is crucial for creating and handling events within the system. This file is
responsible for defining the events and the observers which listen to these events.

## Overview

Magento 2's `events.xml` is typically located under the `etc` directory in a module. The directory structure is as
follows:

```plaintext
app
└── code
    └── Vendor
        └── Module
            └── etc
                ├── events.xml
                └── ...
```

## File Structure

The `events.xml` file uses XML format and generally follows this structure:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="event_name">
        <observer name="observer_name" instance="Vendor\Module\Observer\ObserverClass" method="execute"/>
    </event>
</config>
```

- `event_name` refers to the event's unique name, which will be dispatched by Magento.
- `observer_name` is the unique name of the observer in the context of this event.
- `Vendor\Module\Observer\ObserverClass` is the class responsible for handling the event when it's triggered.
- `method` is the method in the ObserverClass that will be called.

## Defining an Event

Defining an event in the `events.xml` file is as simple as adding an `event` tag with a unique `name` attribute. Here's
an example:

```xml
<event name="catalog_product_save_after">
    <observer name="catalog_product_save_after_observer" instance="Vendor\Module\Observer\ProductSaveAfter"
              method="execute"/>
</event>
```

In this case, the `catalog_product_save_after` event is defined, which will trigger after a product is saved.

## Defining an Observer

Defining an observer for the event involves adding an `observer` tag inside the `event` tag. The `instance` attribute
specifies the class that will handle this event, while the `method` attribute defines the method that will be called.

```xml
<observer name="catalog_product_save_after_observer" instance="Vendor\Module\Observer\ProductSaveAfter"
          method="execute"/>
```

Here, when the `catalog_product_save_after` event triggers, the `execute` method of
the `Vendor\Module\Observer\ProductSaveAfter` class will be called.

## Observer Class

An observer class typically extends `Magento\Framework\Event\ObserverInterface` and implements the `execute` method,
where the event logic resides.

Here's a sample observer class:

```php
<?php

namespace Vendor\Module\Observer;

use Magento\Framework\Event\ObserverInterface;
use Magento\Framework\Event\Observer;

class ProductSaveAfter implements ObserverInterface
{
    public function execute(Observer $observer)
    {
        $product = $observer->getEvent()->getProduct();
        // Handle the event logic here
    }
}
```

## Conclusion

The `events.xml` file plays a crucial role in Magento 2's event-driven programming paradigm. It facilitates interaction
between modules and helps maintain code decoupling, making it easier to modify or extend the functionalities. By
mastering event and observer implementation in Magento 2, developers can build highly flexible and scalable ecommerce
solutions.