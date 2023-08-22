# `layout.xml` Reference Documentation

[TOC]

## Introduction

The layout.xml file is a crucial component of Magento 2's theming system. It provides a way to define the structure and
presentation of a webpage by specifying the block hierarchy, container layout, and block templates. This reference
documentation aims to explain the various elements and attributes that can be used in layout.xml files, along with their
functionalities and how they interact with the overall page rendering process.

## Layout File Structure

A layout.xml file is generally located in the `app/design/frontend/{Vendor}/{Theme}/Magento_Theme/layout` directory of a
Magento 2 theme. It follows a hierarchical structure where the root element is typically `<page>` or `<body>`, and it
can contain multiple nested elements like `<block>`, `<container>`, and `<referenceContainer>`. These elements describe
the various sections, blocks, and containers within the page layout.

## Blocks

Blocks are the building blocks of a layout file. They represent discrete sections of content or functionality on a
webpage. Each block is defined using the `<block>` element, which must have a unique name attribute and can have
optional attributes like `class`, `template`, and `cacheable`.

Example:

```xml
<block name="custom.block" class="Vendor\Namespace\Block\CustomBlock" template="Vendor_Namespace::custom_block.phtml"/>
```

In the above example:

- `name` is a unique identifier for the block within the layout.
- `class` is the PHP class that implements the block's behavior.
- `template` specifies the template file used for rendering the block.

## Containers

Containers are used to group blocks and define their layout within a section of a webpage. Similar to blocks, containers
are represented by the `<container>` element, which also requires a unique name attribute. Containers can have optional
attributes like `htmlTag`, `before`, `after`, and `label`.

Example:

```xml
<container name="custom.container" htmlTag="div" label="Custom Container">
    <block name="custom.block" class="Vendor\Namespace\Block\CustomBlock"
           template="Vendor_Namespace::custom_block.phtml"/>
</container>
```

In the above example, the `<container>` element defines a container named `custom.container`. The `htmlTag` attribute
specifies the HTML tag to be used for rendering the container, and the `label` attribute provides a human-readable label
for the container.

## References

References allow blocks and containers to be rearranged or modified within the layout. They are represented by
the `<referenceContainer>` and `<referenceBlock>` elements. References are useful when a module needs to insert or
modify blocks or containers defined by other modules.

Example:

```xml
<referenceContainer name="header.container">
    <container name="custom.container" htmlTag="div" label="Custom Container" after="logo"/>
</referenceContainer>
```

In the above example, the `<referenceContainer>` element references the existing container named `header.container` and
adds a new container named `custom.container` after the block named `logo` within the `header.container`.

## Attributes

Layout elements like blocks, containers, and references can have various attributes that provide additional control over
their behavior and appearance. Some commonly used attributes
include `htmlTag`, `before`, `after`, `label`, `as`, `output`, and `cacheable`.

Example:

```xml
<block name="custom.block" class="Vendor\Namespace\Block\CustomBlock" template="Vendor_Namespace::custom_block.phtml"
       htmlTag="div" before="-" after="footer.container" label="Custom Block" as="custom.block.alias" output="toHtml"
       cacheable="true"/>
```

In the above example:

- `htmlTag` specifies the HTML tag to be used for rendering the block.
- `before` and `after` determine the block's position relative to other blocks or containers.
- `label` provides a human-readable label for the block.
- `as` allows the block to be referred to by an alias within the layout.
- `output` specifies the method used to render the block's output.
- `cacheable` controls whether the block's output is cacheable.

## Examples

To wrap up this reference documentation, here are a few examples that demonstrate the usage of layout.xml elements and
attributes:

- [Example 1: Adding a new block](examples/example1.xml)
- [Example 2: Modifying an existing container](examples/example2.xml)
- [Example 3: Rearranging blocks using references](examples/example3.xml)

Please refer to the above examples for a more hands-on understanding of how the layout.xml file can be used to define
the structure and presentation of a webpage in Magento 2.

## Conclusion

The layout.xml file is a powerful tool for defining the layout and structure of a webpage in Magento 2. By understanding
the elements, attributes, and their interactions, developers can create flexible and customizable page layouts. This
reference documentation should serve as a comprehensive guide to help you harness the full potential of the layout.xml
file in your Magento 2 theming endeavors.
