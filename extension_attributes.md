# Extension Attributes Reference Documentation

[TOC]

## Introduction

Extension attributes in Magento 2 provide a way to extend the functionality of existing data structures, such as models
or entities, without modifying the original code. This allows developers to add custom data fields to existing objects,
enabling them to store additional information relevant to their specific business requirements.

This reference documentation aims to provide a comprehensive overview of extension attributes in Magento 2, including
how to define, use, and manipulate them. By following the guidelines and examples provided, developers will be able to
effectively leverage extension attributes to enhance their Magento 2 projects.

## 1. Defining Extension Attributes

Extension attributes are defined in `extension_attributes.xml` files located in the `etc` directory of a module. These
XML files specify the structure and behavior of the extension attributes. Each `extension_attributes.xml` file can
define extension attributes for one or more data structures.

To define an extension attribute, you need to specify its name, type, and the data structure it extends.
The `extension_attributes.xml` file follows a hierarchical structure, with a root `<extension_attributes>` element
containing individual `<extension_attribute>` elements for each attribute.

Here's an example of an `extension_attributes.xml` file defining an extension attribute named `custom_attribute` for
the `Magento\Catalog\Api\Data\ProductInterface` data structure:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Api/etc/extension_attributes.xsd">
    <extension_attributes for="Magento\Catalog\Api\Data\ProductInterface">
        <extension_attribute name="custom_attribute" type="string"/>
    </extension_attributes>
</config>
```

In this example, the extension attribute `custom_attribute` is defined as a `string` type. It can now be used to store
additional custom data for products.

## 2. Using Extension Attributes

Once extension attributes are defined, they can be used to store and retrieve custom data for the data structures they
extend. To access an extension attribute, you need to use the corresponding getter and setter methods provided by the
Magento 2 framework.

For instance, using the `custom_attribute` extension attribute defined in the previous example, you can retrieve and set
its value for a product object as follows:

```php
/** @var Magento\Catalog\Api\Data\ProductInterface $product */
$product->setCustomAttribute('custom_attribute', 'some value');

// Get the value of the extension attribute
$value = $product->getCustomAttribute('custom_attribute')->getValue();
```

It is important to note that extension attributes are not automatically persisted to the database. You need to manually
save the object containing the extension attribute for the changes to take effect.

## 3. Manipulating Extension Attributes

Extension attributes can also be manipulated using plugins and observers. Plugins allow you to modify the behavior of
getter and setter methods, while observers enable you to react to changes in extension attribute values.

To create a plugin for an extension attribute, you need to define a class that implements
the `Magento\Framework\Api\ExtensionAttributesInterface` interface. This class should contain the desired logic for the
plugin.

Here's an example of a plugin that modifies the behavior of the `getCustomAttribute` method for the `custom_attribute`
extension attribute:

```php
use Magento\Framework\Api\ExtensionAttributesInterface;

class CustomAttributePlugin
{
    public function afterGetCustomAttribute(
        ExtensionAttributesInterface $subject,
        $result,
        $attributeCode
    ) {
        // Modify the result based on custom logic
        return $modifiedResult;
    }
}
```

Observers, on the other hand, allow you to react to changes in extension attribute values by defining observers in the
module's `events.xml` file. These observers are triggered when extension attributes are modified, allowing you to
perform additional actions.

## 4. Code Examples

To provide further understanding and practical guidance, here are a few code examples showcasing the usage of extension
attributes in Magento 2:

1. Retrieving and setting an extension attribute for a product:

```php
/** @var Magento\Catalog\Api\Data\ProductInterface $product */
$product->setCustomAttribute('custom_attribute', 'some value');

// Get the value of the extension attribute
$value = $product->getCustomAttribute('custom_attribute')->getValue();
```

2. Creating a plugin for an extension attribute:

```php
use Magento\Framework\Api\ExtensionAttributesInterface;

class CustomAttributePlugin
{
    public function afterGetCustomAttribute(
        ExtensionAttributesInterface $subject,
        $result,
        $attributeCode
    ) {
        // Modify the result based on custom logic
        return $modifiedResult;
    }
}
```

3. Defining an observer for extension attribute changes:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="extension_attribute_change_event">
        <observer name="extension_attribute_change_observer"
                  instance="Vendor\Module\Observer\ExtensionAttributeChangeObserver"/>
    </event>
</config>
```

In conclusion, extension attributes in Magento 2 offer a powerful way to extend existing data structures and store
additional custom data. By following the guidelines and examples provided in this reference documentation, developers
will be able to effectively leverage extension attributes in their Magento 2 projects, enhancing the flexibility and
functionality of their applications.
