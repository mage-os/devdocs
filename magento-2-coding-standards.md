# Magento 2 Coding Standards

[TOC]

## Introduction

Magento 2 is a powerful e-commerce platform built on top of PHP. To ensure consistency and maintainability in codebases,
it's crucial to follow coding standards. This document outlines the coding standards specific to Magento 2, covering
various aspects of the development process. By adhering to these standards, developers can produce high-quality code
that is easy to read, understand, and maintain.

## File Structure

A well-organized file structure is crucial for a Magento 2 project. Following a consistent structure helps in easily
locating and managing files. The recommended file structure for a Magento 2 project is as follows:

```
app/
  code/
    <Vendor>/
      <ModuleName>/
        Block/
        Controller/
        etc/
        Helper/
        Model/
        Setup/
        view/
          adminhtml/
          frontend/
  design/
    adminhtml/
    frontend/
  lib/
```

## Naming Conventions

Clear and consistent naming conventions contribute to code readability. Magento 2 follows the following conventions:

- **Classes**: Use PascalCase for class names. For example: `MyCustomModuleBlock`.
- **Methods**: Use camelCase for method names. For example: `myMethod`.
- **Variables**: Use camelCase for variable names. For example: `myVariable`.
- **Constants**: Use uppercase snake_case for constants. For example: `MY_CONSTANT`.
- **Interfaces**: Use the `Interface` suffix for interface names. For example: `MyInterface`.
- **Traits**: Use the `Trait` suffix for trait names. For example: `MyTrait`.

## Coding Style

Consistent coding style improves code readability and maintainability. Magento 2 follows the PSR-12 coding standard,
with a few exceptions. Some key points to consider are:

- **Indentation**: Use four spaces for indentation.
- **Line Length**: Limit lines to a maximum of 120 characters.
- **Braces**: Place opening braces on the same line, but closing braces on a new line.
- **Spacing**: Use a single space after control keywords (`if`, `else`, `for`, etc.), and around operators.

Here's an example illustrating the coding style:

```php
<?php

namespace Vendor\Module\Block;

class MyBlock extends \Magento\Framework\View\Element\Template
{
    protected function _prepareLayout()
    {
        if ($this->isEnabled()) {
            $this->setTemplate('Vendor_Module::my_template.phtml');
        }

        return parent::_prepareLayout();
    }

    public function isEnabled()
    {
        return true;
    }
}
```

## PHP Code Sniffers

To enforce coding standards automatically, you can use PHP code sniffers like PHP_CodeSniffer or Magento's ECGM2. These
tools analyze the code against configured rules and highlight any violations.

For example, to check coding standards using PHP_CodeSniffer, run the following command:

```
vendor/bin/phpcs --standard=PSR12 app/code/Vendor/Module/
```

## Magento Specific Standards

Magento 2 has its own set of coding standards specific to module development. Let's discuss a few important ones:

### Module Structure

A well-structured module enhances code organization. A typical module follows this structure:

```
app/
  code/
    <Vendor>/
      <ModuleName>/
        etc/
          module.xml
        registration.php
```

- **`etc/module.xml`**: Contains module configuration.
- **`registration.php`**: Registers the module.

### Dependency Injection (DI)

Magento 2 heavily relies on dependency injection to manage object dependencies. Following DI best practices ensures code
maintainability and testability.

Here's an example of injecting a class dependency in the constructor:

```php
<?php

namespace Vendor\Module\Model;

class MyModel
{
    private $dependency;

    public function __construct(
        \Vendor\OtherModule\Model\Dependency $dependency
    ) {
        $this->dependency = $dependency;
    }

    public function myMethod()
    {
        $this->dependency->doSomething();
    }
}
```

### Layout XML Files

Layout XML files are used to define the structure of pages in Magento 2. Following standards for layout XML files
ensures consistency and readability.

Here's an example of a layout XML file:

```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Vendor\Module\Block\MyBlock" name="my_block" template="Vendor_Module::my_template.phtml"/>
        </referenceContainer>
    </body>
</page>
```

### Database Schema

Magento 2 uses declarative database schema definitions to manage database structures. Following the standards for
defining database schemas ensures maintainability and compatibility with upgrade scripts.

Here's an example of a database schema definition:

```xml
<?xml version="1.0"?>
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="my_table" resource="default" engine="innodb" comment="My Table">
        <column xsi:type="smallint" name="id" nullable="false" unsigned="true" identity="true" comment="ID"/>
        <column xsi:type="varchar" name="name" nullable="false" length="255" comment="Name"/>
        <constraint xsi:type="primary" referenceId="PRIMARY">
            <column name="id"/>
        </constraint>
    </table>
</schema>
```

## Conclusion

Adhering to Magento 2 coding standards ensures code consistency and maintainability. In this document, we covered file
structure, naming conventions, coding style, and Magento-specific standards. By following these guidelines, developers
can create high-quality Magento 2 code that is easier to understand, maintain, and scale.
