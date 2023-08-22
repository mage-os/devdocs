# `menu.xml` Reference Documentation

[TOC]

## Introduction

The `menu.xml` file is an important configuration file in Magento 2 that defines the structure and content of menu items
in your store. It is located in the `etc/adminhtml` directory of your module or theme. This file is used to create or
modify menus in the Magento admin panel.

## Menu Structure

The `menu.xml` file uses XML tags to define the structure of the menu. Each menu item is created as a `<add>` tag within
the `<menu>` tag. Here is an example of a simple menu structure:

```xml
<config>
    <menu>
        <add id="Vendor_Module::menu_item1"
             title="Menu Item 1"
             module="Vendor_Module"
             sortOrder="10"
             parent="Magento_Backend::content"
             action="module/controller/action"/>
        <add id="Vendor_Module::menu_item2"
             title="Menu Item 2"
             module="Vendor_Module"
             sortOrder="20"
             parent="Vendor_Module::menu_item1"
             resource="Vendor_Module::resource"/>
    </menu>
</config>
```

In this example, we have two menu items: "Menu Item 1" and "Menu Item 2".

- The `id` attribute uniquely identifies each menu item. It follows the format `Vendor_Module::menu_item_id`,
  where `Vendor_Module` is the module name and `menu_item_id` is a unique identifier for the menu item.
- The `title` attribute sets the display name of the menu item.
- The `module` attribute specifies the module that owns the menu item.
- The `sortOrder` attribute determines the order in which the menu items are displayed.
- The `parent` attribute defines the parent menu item of the current menu item. The `parent` attribute value should be
  set to the `id` of the parent menu item.
- The `action` attribute specifies the controller and action that will be executed when the menu item is clicked.
- The `resource` attribute restricts access to the menu item based on user roles and permissions.

## Menu Item Configuration

Each menu item can be further configured using additional XML tags within the `<add>` tag. Here are some commonly used
configuration options:

### ACL Resource

The `<resource>` tag is used to specify the ACL resource that controls access to the menu item. It is recommended to
define a unique ACL resource for each menu item to manage user permissions effectively. For example:

```xml
<add id="Vendor_Module::menu_item3"
     title="Menu Item 3"
     module="Vendor_Module"
     sortOrder="30"
     parent="Vendor_Module::menu_item2">
    <resource>Vendor_Module::resource</resource>
</add>
```

### Menu Item Icons

You can add icons to your menu items using the `<add>` tag's `resource` attribute. Magento 2 supports a wide range of
icons provided by the Font Awesome library. For example:

```xml
<add id="Vendor_Module::menu_item4"
     title="Menu Item 4"
     module="Vendor_Module"
     sortOrder="40"
     parent="Vendor_Module::menu_item3"
     action="module/controller/action">
    <resource>Vendor_Module::resource</resource>
    <arguments>
        <argument name="icon" xsi:type="string">fa-icon-name</argument>
    </arguments>
</add>
```

Replace `fa-icon-name` with the desired Font Awesome icon class name.

### Menu Item Submenus

You can create submenus by adding multiple levels of menu items. Each submenu is defined by adding a nested `<add>` tag
within the parent menu item's `<add>` tag. For example:

```xml
<add id="Vendor_Module::menu_item5"
     title="Menu Item 5"
     module="Vendor_Module"
     sortOrder="50"
     parent="Magento_Backend::content">
    <add id="Vendor_Module::menu_item6"
         title="Menu Item 6"
         module="Vendor_Module"
         sortOrder="10"
         parent="Vendor_Module::menu_item5"
         action="module/controller/action">
        <resource>Vendor_Module::resource</resource>
    </add>
</add>
```

In this example, "Menu Item 6" is a submenu of "Menu Item 5".

## Conclusion

The `menu.xml` file is a crucial component in defining the structure and content of menus in the Magento admin panel. By
understanding its structure and configuration options, you can create customized menus that fit your specific needs. Use
the provided examples and code snippets as a reference to help you create and modify menu items effectively.
