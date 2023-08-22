# Observers Documentation

[TOC]

## Introduction

Observers are an essential part of the event-driven architecture in Magento 2. They allow you to hook into specific
events and execute custom code when those events are dispatched. This allows for flexibility and customization without
modifying core code. In this documentation, we will explore the concept of observers in Magento 2 and provide examples
to help you understand and implement them in your own projects.

## Observer Basics

Observers in Magento 2 are PHP classes that implement the `\Magento\Framework\Event\ObserverInterface` interface. This
interface defines a single method, `execute()`, which is called when the observed event is dispatched.

Here's a basic example of an observer class:

```php
namespace Vendor\Module\Observer;

use Magento\Framework\Event\ObserverInterface;

class MyObserver implements ObserverInterface
{
    public function execute(\Magento\Framework\Event\Observer $observer)
    {
        // Custom code here
    }
}
```

The `execute()` method is where you provide the logic for your observer. The `$observer` parameter contains information
about the event being observed, including the event name, event data, and the object that dispatched the event.

## Registering Observers

To make your observer active, you need to register it in a Magento 2 module's `etc/events.xml` file. This XML file
defines which events your observer is listening to and associates the observer class with those events.

Here's an example of registering an observer in `etc/events.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="some_event_name">
        <observer name="my_observer_name" instance="Vendor\Module\Observer\MyObserver"/>
    </event>
</config>
```

In this example, the observer `MyObserver` is registered for the `some_event_name` event.

## Dispatching Events

To trigger your observer, you need to dispatch the corresponding event. Magento 2 provides various ways to dispatch
events, depending on the context and purpose.

Here's an example of dispatching an event:

```php
use Magento\Framework\Event\ManagerInterface as EventManager;

class SomeClass
{
    private $eventManager;

    public function __construct(EventManager $eventManager)
    {
        $this->eventManager = $eventManager;
    }

    public function doSomething()
    {
        // Some business logic

        $eventData = ['param1' => 'value1', 'param2' => 'value2'];

        $this->eventManager->dispatch('some_event_name', $eventData);

        // Continue with other operations
    }
}
```

In this example, the event with the name `some_event_name` is dispatched using the `$eventManager->dispatch()` method.
The `$eventData` array can contain any additional data you want to pass to the observer.

## Observer Execution

When an event is dispatched, Magento 2 will automatically trigger the `execute()` method of all registered observers for
that event. The order of execution is determined by the order in which the observers are registered.

If you have multiple observers for the same event, you can define the execution order by setting the `sequence`
attribute in the observer registration. Observers with lower sequence values will execute first.

```xml
<observer name="first_observer" instance="Vendor\Module\Observer\FirstObserver" sequence="10"/>
<observer name="second_observer" instance="Vendor\Module\Observer\SecondObserver" sequence="20"/>
```

In this example, `FirstObserver` will execute before `SecondObserver` due to the lower sequence value.

## Observer Example

Let's consider a practical example to illustrate how observers work. Suppose you want to send a notification email to
the customer whenever a new order is placed in your Magento 2 store.

First, create an observer class to handle the logic:

```php
namespace Vendor\Module\Observer;

use Magento\Framework\Event\ObserverInterface;
use Magento\Framework\Mail\Template\TransportBuilder;
use Magento\Store\Model\StoreManagerInterface;

class NewOrderObserver implements ObserverInterface
{
    private $transportBuilder;
    private $storeManager;

    public function __construct(
        TransportBuilder $transportBuilder,
        StoreManagerInterface $storeManager
    ) {
        $this->transportBuilder = $transportBuilder;
        $this->storeManager = $storeManager;
    }

    public function execute(\Magento\Framework\Event\Observer $observer)
    {
        $order = $observer->getData('order');

        $storeId = $order->getStoreId();
        $store = $this->storeManager->getStore($storeId);

        $templateVars = [
            'order' => $order,
            'store' => $store
        ];

        $this->transportBuilder->setTemplateIdentifier('new_order_email_template')
            ->setTemplateOptions(['area' => 'frontend', 'store' => $storeId])
            ->setTemplateVars($templateVars)
            ->setFrom('general')
            ->addTo($order->getCustomerEmail())
            ->getTransport()
            ->sendMessage();
    }
}
```

In this example, the `execute()` method retrieves the order object from the observer data and sends an email using
the `TransportBuilder`.

Next, register the observer in your module's `etc/events.xml` file:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="sales_order_place_after">
        <observer name="new_order_observer" instance="Vendor\Module\Observer\NewOrderObserver" />
    </event>
</config>
```

Now, whenever a new order is placed (`sales_order_place_after` event), the `NewOrderObserver` will be triggered, sending
an email notification to the customer.

## Conclusion

Observers in Magento 2 provide a powerful way to customize and extend the functionality of your store without modifying
the core code. By registering observers for specific events, you can execute custom code at the right time and integrate
with other modules seamlessly. This documentation has covered the basics of observers, including their implementation,
registration, and execution. With this knowledge, you can leverage observers to build flexible and customizable
solutions in your Magento 2 projects.
