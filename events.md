# Event Documentation

[TOC]

This documentation provides a comprehensive guide on events in Magento 2, specifically tailored for developers familiar
with PHP and Magento 2. Events in Magento 2 allow you to extend the functionality of the core system by injecting custom
code at specific points in the application flow. By understanding and utilizing events effectively, you can enhance the
flexibility and modularity of your Magento 2 stores.

## Table of Contents

1. [Introduction to Events](#introduction-to-events)
2. [Using Events in Magento 2](#using-events-in-magento-2)
3. [Event Dispatching](#event-dispatching)
4. [Event Observers](#event-observers)
5. [Creating Custom Events](#creating-custom-events)
6. [Summary](#summary)

## Introduction to Events

Events in Magento 2 follow the Observer design pattern, allowing you to observe and respond to specific events triggered
during the execution of the system. These events serve as hooks, enabling you to inject custom code before, during, or
after the execution of predefined processes.

## Using Events in Magento 2

To understand how events work in Magento 2, let's explore a basic example. Suppose you want to add a custom logging
functionality whenever a new customer account is created. By leveraging events, you can achieve this without modifying
the core code.

### Event Dispatching

In Magento 2, events are dispatched using the `Magento\Framework\Event\ManagerInterface` interface. To dispatch an
event, you need to follow these steps:

1. Determine the event name to be dispatched. In this example, we will use the event `customer_register_success`.

2. Inject the `ManagerInterface` using dependency injection in your class:

```php
protected $eventManager;

public function __construct(
    \Magento\Framework\Event\ManagerInterface $eventManager
) {
    $this->eventManager = $eventManager;
}
```

3. Dispatch the event at the appropriate place in your code:

```php
$this->eventManager->dispatch('customer_register_success', ['customer' => $customer]);
```

By dispatching the event `customer_register_success` and passing the `customer` object, we allow other observers to
react to this event.

### Event Observers

Observers are responsible for observing events and executing specific actions in response. Magento 2 provides a
convenient way to define observers using XML configuration. Let's create an observer for our example:

1. Create a new XML file `events.xml` in your module's `etc` directory:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="customer_register_success">
        <observer name="custom_logger" instance="Vendor\Module\Observer\CustomLogger"/>
    </event>
</config>
```

2. Create the observer class `CustomLogger`:

```php
namespace Vendor\Module\Observer;

use Magento\Framework\Event\ObserverInterface;
use Psr\Log\LoggerInterface;

class CustomLogger implements ObserverInterface
{
    protected $logger;

    public function __construct(LoggerInterface $logger)
    {
        $this->logger = $logger;
    }

    public function execute(\Magento\Framework\Event\Observer $observer)
    {
        $customer = $observer->getData('customer');
        $this->logger->info('New customer registered: ' . $customer->getName());
    }
}
```

In this example, we observe the `customer_register_success` event and log a message containing the name of the customer
who registered using the `LoggerInterface`.

### Creating Custom Events

While Magento 2 provides a wide range of predefined events, you can also create custom events to fit your specific
needs. To create a custom event, follow these steps:

1. Create a new XML file `events.xml` in your module's `etc` directory:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="custom_event">
        <observer name="custom_observer" instance="Vendor\Module\Observer\CustomObserver"/>
    </event>
</config>
```

2. Create the observer class `CustomObserver`:

```php
namespace Vendor\Module\Observer;

use Magento\Framework\Event\ObserverInterface;

class CustomObserver implements ObserverInterface
{
    public function execute(\Magento\Framework\Event\Observer $observer)
    {
        // Custom logic goes here
    }
}
```

In this example, we create a custom event named `custom_event` and associate it with the observer `CustomObserver`.

## Summary

Congratulations! You have learned the fundamentals of events in Magento 2. By dispatching and observing events, you can
extend the core functionality of the system without modifying the core code. This approach enhances modularity and
allows for easier maintenance and upgrades. Remember to refer to the official Magento 2 documentation for more detailed
information on specific events and their usage. Happy coding!
