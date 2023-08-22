# Widget.xml Reference Documentation

## Overview

The `widget.xml` file is an important configuration file in Magento 2 that defines the behavior and properties of
widgets. Widgets are reusable components that can be placed in various areas of a Magento store to display dynamic
content. This reference documentation will provide a detailed explanation of the `widget.xml` file and its various
elements.

## XML Structure

The `widget.xml` file follows a structured XML format. It consists of a root `<widgets>` element, which contains one or
more `<widget>` elements. Each `<widget>` element represents a specific widget and contains its configuration details.
Let's examine the key elements and attributes of the `widget.xml` file.

## `<widget>` Element

The `<widget>` element is the main building block of the `widget.xml` file. It defines a widget and its properties. Here
is an example:

```xml
<widget id="example_widget" class="Vendor\ExampleWidget\Block\Widget\Example">
    <label translate="true">Example Widget</label>
    <description translate="true">This is an example widget.</description>
    <parameters>
        <!-- Widget parameters go here -->
    </parameters>
    <containers>
        <!-- Widget containers go here -->
    </containers>
    <requiredParameters>
        <!-- Required widget parameters go here -->
    </requiredParameters>
    <supportedBlocks>
        <!-- Supported block types go here -->
    </supportedBlocks>
</widget>
```

Let's break down the attributes and child elements of the `<widget>` element:

- `id` (required): An identifier for the widget. It should be unique within the scope of the module.
- `class` (required): The fully qualified class name of the widget block.
- `<label>` (required): A user-friendly label for the widget. It can be translated using the `translate` attribute.
- `<description>` (optional): A description of the widget. It can also be translated.
- `<parameters>` (optional): This element contains one or more `<parameter>` elements that define the configuration
  options for the widget.
- `<containers>` (optional): This element contains one or more `<container>` elements that define where the widget can
  be placed in the layout.
- `<requiredParameters>` (optional): This element contains one or more `<parameter>` elements that must be configured
  when using the widget.
- `<supportedBlocks>` (optional): This element contains one or more `<block>` elements that specify the block types
  supported by the widget.

## `<parameter>` Element

The `<parameter>` element defines a configuration option for the widget. It can be of various types, such as text,
select, boolean, etc. Here is an example:

```xml
<parameters>
    <parameter name="title" xsi:type="text" required="true">
        <label translate="true">Title</label>
        <sort_order>10</sort_order>
    </parameter>
    <parameter name="show_price" xsi:type="boolean">
        <label translate="true">Show Price</label>
        <sort_order>20</sort_order>
    </parameter>
    <!-- More parameters -->
</parameters>
```

Let's examine the attributes and child elements of the `<parameter>` element:

- `name` (required): The name of the parameter. It should be unique within the widget.
- `xsi:type` (required): The type of the parameter. It determines the input field or UI component used to configure the
  parameter.
- `required` (optional): Specifies whether the parameter is required or not.
- `<label>` (required): A user-friendly label for the parameter. It can be translated using the `translate` attribute.
- `<sort_order>` (optional): Specifies the order in which the parameters are displayed in the widget configuration form.

## `<container>` Element

The `<container>` element defines a layout container where the widget can be placed. It specifies the block name and
template file for rendering the widget. Here is an example:

```xml
<containers>
    <container name="content.top">
        <template name="widget/example.phtml">
        </template>
    </container>
    <!-- More containers -->
</containers>
```

Let's examine the attributes and child elements of the `<container>` element:

- `name` (required): The name of the container. It should match a valid layout container defined in the theme or module.
- `<template>` (required): The name of the template file used to render the widget in the container.

## `<block>` Element

The `<block>` element specifies the block types supported by the widget. The supported blocks can be used as child
blocks within the widget. Here is an example:

```xml
<supportedBlocks>
    <block name="catalog/product_list"/>
    <block name="cms/block"/>
    <!-- More supported blocks -->
</supportedBlocks>
```

Let's examine the attributes of the `<block>` element:

- `name` (required): The name of the supported block type. It should match a valid block type in Magento.

## Conclusion

The `widget.xml` file is a powerful configuration file in Magento 2 that allows you to define and customize widgets. By
understanding the structure and elements of `widget.xml`, you can create dynamic and reusable components for your
Magento store. Make sure to refer to this documentation for guidance when working with `widget.xml` and leverage the
provided examples to enhance your understanding.
