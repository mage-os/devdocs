# `events.xml` Reference Documentation

The `events.xml` file is used in Magento 2 to define event listeners and their corresponding observers. Event listeners
are used to perform specific actions or modifications when certain events occur within the Magento system. They allow
you to extend the functionality of Magento without modifying its core code.

## File Location

The `events.xml` file is typically located in the `etc` directory of a Magento module. For example, if you have a module
named `MyModule`, the `events.xml` file should be placed in the following location: `app/code/MyModule/etc/events.xml`.

## Basic Structure

The basic structure of the `events.xml` file consists of the `<config>` root element, which encapsulates one or
more `<event>` elements. Each `<event>` element defines a specific event and its corresponding observers.

Here is an example of a basic `events.xml` file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="my_custom_event">
        <observer name="my_custom_observer" instance="MyModule\MyObserver" method="execute"/>
    </event>
</config>
```

In this example, we define a custom event named `my_custom_event`. When this event is triggered, it will execute the
observer `MyModule\MyObserver` and call its `execute` method.

## Defining Events

To define an event in the `events.xml` file, you need to specify its name using the `name` attribute of the `<event>`
element. The event name should be unique and typically follows a "module_name.event_name" format.

Here is an example of an event definition:

```xml

<event name="catalog_product_save_after">
    <!-- Observer definitions go here -->
</event>
```

In this example, we define an event named `catalog_product_save_after`. This event is triggered after a product is saved
in the admin panel.

## Defining Observers

Observers are classes that contain the logic to be executed when an event is triggered. To define an observer, you need
to specify its name, instance, and method using the `<observer>` element within the `<event>` element.

Here is an example of an observer definition:

```xml

<observer name="my_custom_observer" instance="MyModule\MyObserver" method="execute"/>
```

In this example, we define an observer named `my_custom_observer`. It is an instance of the `MyModule\MyObserver` class,
and when the event is triggered, the `execute` method of this observer will be called.

## Passing Data to Observers

You can pass additional data to observers by including `<data>` elements within the `<observer>` element. Each `<data>`
element represents a key-value pair that can be accessed in the observer's execute method.

Here is an example of passing data to an observer:

```xml

<observer name="my_custom_observer" instance="MyModule\MyObserver" method="execute">
    <data name="my_custom_data">Some Value</data>
</observer>
```

In this example, we pass the value "Some Value" to the observer by defining a `<data>` element with the name "
my_custom_data". This data can be accessed in the observer's execute method using the `$observer` parameter.

```php
public function execute(\Magento\Framework\Event\Observer $observer)
{
    $myCustomData = $observer->getData('my_custom_data');
    // Use the $myCustomData variable here
}
```

## Multiple Observers for an Event

You can have multiple observers for a single event by including multiple `<observer>` elements within the `<event>`
element.

Here is an example of multiple observers for an event:

```xml

<event name="my_custom_event">
    <observer name="observer_1" instance="MyModule\Observer\Observer1" method="execute"/>
    <observer name="observer_2" instance="MyModule\Observer\Observer2" method="execute"/>
</event>
```

In this example, when the `my_custom_event` is triggered, both `Observer1` and `Observer2` will be executed in the order
they are defined.

## Conclusion

The `events.xml` file is a powerful tool in Magento 2 for extending functionality and reacting to specific events within
the system. By understanding its structure and how to define events and observers, you can customize Magento to meet
your specific business requirements.

# Events.xml Reference Documentation

## Overview

The `events.xml` file is a crucial component in the Magento 2 development framework. It plays a vital role in triggering
events and executing corresponding actions within a Magento system. This file is a powerful tool that enables developers
to extend and customize the behavior of Magento's core functionality, without modifying the original code.

## File Location

The `events.xml` file is typically located in the `etc` directory of a Magento module. For example, if you have a custom
module named "MyModule," the file path would be `app/code/Vendor/MyModule/etc/events.xml`.

## Structure

The structure of `events.xml` follows a simple XML format. It consists of two main elements: `event` and `observer`.

### Event

The `event` element represents a specific event that Magento triggers during its execution. It contains an `name`
attribute that defines the event name and an optional `disabled` attribute that allows you to disable the event without
removing it from the file.

Here's an example of an event declaration in `events.xml`:

```xml

<event name="my_custom_event" disabled="true"/>
```

### Observer

The `observer` element specifies the action to be executed when the associated event is triggered. It contains a
mandatory `name` attribute, which represents a unique identifier for the observer. Additionally, it includes
a `instance` attribute that defines the class responsible for handling the event. The `instance` attribute should be set
using the format `Vendor\Module\Observer\ClassName`.

Here's an example of an observer declaration in `events.xml`:

```xml

<observer name="my_custom_observer" instance="Vendor\Module\Observer\MyObserver"/>
```

## Usage

To utilize `events.xml` effectively, you need to understand how events and observers work together. When an event is
triggered, all associated observers are executed in the order they are declared in the `events.xml` file.

### Creating an Event

To create a new event, you need to add an `event` element to the `events.xml` file. When naming the event, it is
recommended to use a unique and descriptive identifier that reflects its purpose.

For example, let's create a custom event called `my_custom_event`:

```xml

<event name="my_custom_event"/>
```

### Creating an Observer

To create an observer for the event, add an `observer` element within the corresponding `event` element. Provide a
unique name for the observer and link it to the relevant class using the `instance` attribute.

Here's an example of creating an observer `my_custom_observer`:

```xml

<event name="my_custom_event">
    <observer name="my_custom_observer" instance="Vendor\Module\Observer\MyObserver"/>
</event>
```

### Implementing the Observer Class

To implement the observer functionality, create a PHP class that corresponds to the `instance` attribute value specified
in the `events.xml` file. This class should extend the `Magento\Framework\Event\Observer` class.

Below is an example of an observer class that logs a message when the `my_custom_event` is triggered:

```php
namespace Vendor\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;
use Psr\Log\LoggerInterface;

class MyObserver implements ObserverInterface
{
    protected $logger;

    public function __construct(LoggerInterface $logger)
    {
        $this->logger = $logger;
    }

    public function execute(Observer $observer)
    {
        $this->logger->info('Custom event triggered!');
    }
}
```

### Dispatching the Event

To trigger the event and execute the associated observers, you can use the `Magento\Framework\Event\Manager` class.
Inject this class into the desired location, and call the `dispatch` method, passing the event name as a parameter.

Here's an example of dispatching the `my_custom_event`:

```php
namespace Vendor\Module\Block;

use Magento\Framework\View\Element\Template;
use Magento\Framework\Event\Manager;

class MyBlock extends Template
{
    protected $eventManager;

    public function __construct(Template\Context $context, Manager $eventManager)
    {
        parent::__construct($context);
        $this->eventManager = $eventManager;
    }

    public function executeCustomEvent()
    {
        $this->eventManager->dispatch('my_custom_event');
    }
}
```

## Conclusion

The `events.xml` file empowers developers to extend and customize the behavior of Magento 2 by defining events and their
corresponding observers. By understanding its structure and usage, you can leverage this powerful mechanism to modify
core functionality without modifying the original code. Remember to follow best practices when creating events and
observers, and test thoroughly to ensure seamless integration into your Magento system.
