# Plugin Documentation

[TOC]

## Introduction

Plugins in Magento 2 provide a way to extend and modify the behavior of existing code without directly modifying it.
This allows developers to customize Magento 2's functionality without the need for modifying core files, ensuring easier
upgrades and compatibility with other extensions. In this documentation, we will explore the concept of plugins, their
usage, and provide practical examples for better understanding.

## Plugin Basics

A plugin, also known as an interceptor, is a class that modifies the behavior of a public method in a target class. It
allows you to execute custom code before, after, or around the execution of the original method, without modifying the
original code directly. This can be useful for adding new functionality, logging, caching, or modifying the input/output
of a method.

## Plugin Types

There are three types of plugins that can be used in Magento 2: `before`, `after`, and `around`. Let's discuss each type
in more detail.

### 1. Before Plugin

A `before` plugin allows you to execute custom code before the execution of the target method. This is useful for
intercepting the input parameters and modifying them if needed. For example, let's say we have a
method `doSomething($param1, $param2)` in a class `TargetClass`. We can create a `before` plugin to intercept the
execution of this method and modify the input parameters:

```php
class BeforePlugin
{
    public function beforeDoSomething($subject, $param1, $param2)
    {
        // Modify $param1 and $param2 here
        $param1 = 'Modified ' . $param1;
        $param2 += 10;
        
        // You can also modify the subject instance itself if needed
        $subject->setSomeProperty('Modified Value');
        
        // Always return the modified parameters
        return [$param1, $param2];
    }
}
```

### 2. After Plugin

An `after` plugin allows you to execute custom code after the execution of the target method. This is useful for
intercepting the return value of the method and modifying it if needed. For example, let's say we have a
method `doSomething()` in a class `TargetClass` that returns a value. We can create an `after` plugin to intercept the
execution of this method and modify the return value:

```php
class AfterPlugin
{
    public function afterDoSomething($subject, $result)
    {
        // Modify $result here
        $result = 'Modified ' . $result;
        
        // Return the modified result
        return $result;
    }
}
```

### 3. Around Plugin

An `around` plugin allows you to execute custom code before and/or after the execution of the target method. This is
useful when you want to completely override the original method's behavior or conditionally execute custom code. For
example, let's say we have a method `doSomething()` in a class `TargetClass`. We can create an `around` plugin to
intercept the execution of this method and modify its behavior:

```php
class AroundPlugin
{
    public function aroundDoSomething($subject, $proceed)
    {
        // Code to execute before the original method
        
        // Call the original method using $proceed()
        $result = $proceed();
        
        // Code to execute after the original method
        
        // Modify $result if needed
        
        // Return the modified result
        return $result;
    }
}
```

## Plugin Configuration

To use a plugin in Magento 2, you need to define its configuration in your module's `di.xml` file. Here's an example of
how to configure a plugin for a class `TargetClass`:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="TargetClass">
        <plugin name="before-plugin" type="Vendor\Module\Plugin\BeforePlugin" sortOrder="10" disabled="false"/>
        <plugin name="after-plugin" type="Vendor\Module\Plugin\AfterPlugin" sortOrder="20" disabled="false"/>
        <plugin name="around-plugin" type="Vendor\Module\Plugin\AroundPlugin" sortOrder="30" disabled="false"/>
    </type>
</config>
```

Make sure to replace `TargetClass`, `Vendor\Module`, and plugin names with your actual class and module names.

## Conclusion

Plugins are a powerful tool in Magento 2 that allows you to modify the behavior of existing code without directly
modifying it. By leveraging the `before`, `after`, and `around` plugin types, you can customize Magento's functionality
to meet your specific requirements. Remember to configure your plugins in the `di.xml` file of your module. Happy plugin
development!
