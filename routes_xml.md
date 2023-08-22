# `routes.xml` Reference Documentation

[TOC]

## Introduction

The `routes.xml` file is an essential configuration file in Magento 2, particularly when it comes to defining and
managing custom routes. This file plays a crucial role in routing HTTP requests to the appropriate controllers in your
Magento 2 module. In this document, you will learn how to effectively utilize the `routes.xml` file to create and manage
routes in your Magento 2 module.

## File Location and Structure

The `routes.xml` file resides in the `etc/frontend` or `etc/adminhtml` directory of your module. The exact file path
depends on whether your module is for the frontend or admin area of Magento 2. The file follows a structured XML format
and consists of multiple elements that define the routes and their associated controllers.

Here is an example of the basic structure of a `routes.xml` file:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="[ROUTER_ID]">
        <route id="[ROUTE_ID]" frontName="[FRONT_NAME]">
            <module name="[MODULE_NAME]"/>
        </route>
    </router>
</config>
```

Let's dive into each of these elements to gain a deeper understanding.

## `<config>` Element

The `<config>` element is the root element of the `routes.xml` file. It defines the XML namespace and specifies the
schema location using the `xmlns:xsi` and `xsi:noNamespaceSchemaLocation` attributes, respectively. You don't need to
modify these attributes as they refer to the default schema provided by Magento.

## `<router>` Element

The `<router>` element is used to define the router ID, which is a unique identifier for the router. The router ID is
used to group related routes together. In most cases, you will use either `standard` or `admin` as the router ID. For
example, `<router id="standard">` defines a router for the frontend area, whereas `<router id="admin">` defines a router
for the admin area.

## `<route>` Element

The `<route>` element represents a specific route in Magento 2. It consists of three attributes: `id`, `frontName`, and
optional `disabled`.

- The `id` attribute specifies a unique identifier for the route and is used internally by Magento to identify and match
  the incoming requests.
- The `frontName` attribute defines the URL segment that precedes the action name in the URL. For example,
  if `frontName="custom"`, the URL `https://example.com/custom/index/index` will map to the `Index/Index` action of the
  associated controller.
- The optional `disabled` attribute, when set to `true`, disables the route. This can be useful when you want to
  temporarily deactivate a route without removing it from the `routes.xml` file.

## `<module>` Element

The `<module>` element is a child element of the `<route>` element, and it specifies the name of the module that handles
the route. The `name` attribute should match the module's name as defined in its `module.xml` file.

## Example

Let's walk through an example to illustrate how the `routes.xml` file works. Assume we have a module
named `Acme_CustomModule` that needs to define a custom route for frontend pages.

Here is the `routes.xml` file for this module:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route id="custom" frontName="custom">
            <module name="Acme_CustomModule"/>
        </route>
    </router>
</config>
```

In this example, we defined a route with the `id` of "custom" and `frontName` of "custom". The associated module is
specified as `Acme_CustomModule`.

Now, let's assume we have a controller named `Index` inside the `Acme\CustomModule\Controller\Index` namespace. With
this `routes.xml` configuration, the URL `https://example.com/custom/index/index` will map to the `Index`
controller's `index` action.

## Conclusion

The `routes.xml` file is a crucial component for defining and managing routes in Magento 2. By carefully configuring
this file, you can easily map incoming HTTP requests to the appropriate controllers within your module. Understanding
the structure and elements of the `routes.xml` file will empower you to create custom routes efficiently. Remember to
adhere to the XML structure and use correct attribute values to ensure proper routing functionality.
