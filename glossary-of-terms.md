# Glossary of Terms

[TOC]

This glossary contains explanations of commonly used terms in the context of programming, PHP, and Magento 2.

## 1. PHP

### 1.1 Variable

A variable in PHP is a named container that can hold a value. It is used to store and manipulate data during the
execution of a program. Variables are declared using the `$` symbol followed by the variable name and an optional
initial value.

Example:

```php
$name = "John";
$age = 25;
```

### 1.2 Function

A function in PHP is a block of reusable code that performs a specific task. It encapsulates a series of statements and
can be called multiple times from different parts of a program. Functions can accept parameters and return values.

Example:

```php
function calculateSum($a, $b) {
    return $a + $b;
}
```

### 1.3 Array

An array in PHP is a data structure that can store multiple values under a single variable name. It allows you to group
related data together. PHP supports both indexed and associative arrays. Indexed arrays store values with numeric keys,
while associative arrays use string keys.

Example:

```php
$fruits = ["apple", "banana", "orange"];
$person = ["name" => "John", "age" => 25];
```

### 1.4 Class

A class in PHP is a blueprint for creating objects. It defines the properties (variables) and methods (functions) that
an object of that class can have. Objects are instances of classes and can be created using the `new` keyword.

Example:

```php
class Car {
    public $brand;
    public function startEngine() {
        echo "Engine started!";
    }
}

$myCar = new Car();
$myCar->brand = "Toyota";
$myCar->startEngine();
```

## 2. Magento 2

### 2.1 Module

A module in Magento 2 is a self-contained unit that adds specific functionality to the Magento system. It consists of
code, configuration files, templates, and other resources. Modules can be developed by Magento or third-party developers
to extend or modify the behavior of the platform.

Example:

```
app/code/Vendor/Module
```

### 2.2 Block

A block in Magento 2 is a PHP class responsible for generating and managing the presentation logic of a specific part of
a web page. It is typically used to retrieve and process data from models and provide it to templates for rendering.
Blocks are organized in a hierarchical structure and can have child blocks.

Example:

```php
class MyBlock extends \Magento\Framework\View\Element\Template
{
    public function getHelloMessage()
    {
        return "Hello, Magento!";
    }
}
```

### 2.3 Layout

A layout in Magento 2 is an XML file that defines the structure and appearance of a web page. It specifies the blocks,
containers, and their positions within the page. Layout files are used to control the overall layout of a Magento store
and determine which blocks to display on different pages.

Example:

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Vendor\Module\Block\MyBlock" name="my_block" template="Vendor_Module::my_block.phtml"/>
        </referenceContainer>
    </body>
</page>
```

### 2.4 Plugin

A plugin in Magento 2 is a class that intercepts and modifies the behavior of a public method of another class (the
target class). It allows you to add custom logic before, after, or around the execution of the target method. Plugins
are used for extending or customizing the functionality of Magento without modifying the original code.

Example:

```php
class MyPlugin
{
    public function beforeGetName(\Magento\Catalog\Model\Product $product)
    {
        return ['My custom name'];
    }
}
```

These are just a few of the many terms and concepts used in programming, PHP, and Magento 2. By understanding and
familiarizing yourself with these terms, you'll be better equipped to work with and understand the code and
documentation within the PHP and Magento 2 ecosystems.
