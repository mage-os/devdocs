# `system.xml` Reference Documentation

[TOC]

System.xml is a powerful configuration file used in PHP and Magento 2 to define system-level settings and
configurations. This file plays a crucial role in customizing the behavior and appearance of applications built on these
platforms. In this reference guide, we will explore the structure, syntax, and usage of system.xml, along with practical
examples to demonstrate its capabilities.

## Introduction to System.xml

System.xml is a configuration file that allows developers to define custom settings and configurations for PHP
applications, particularly those built on the Magento 2 platform. It provides a structured approach to manage various
aspects of application behavior, such as enabling/disabling features, setting default values, and specifying user
interface options.

The system.xml file is typically located in the "etc" directory of a Magento 2 module, following the file naming
convention: `<Module_Root>/etc/adminhtml/system.xml`. This file is XML-based, which means it follows the XML syntax and
requires strict adherence to its rules.

## Structure and Syntax

The system.xml file follows a hierarchical structure that consists of sections, groups, and fields. The root element of
this file is `<config>`, and it contains one or more `<section>` elements, each representing a separate configuration
section.

Here is an example of a basic system.xml file structure:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Config:etc/system_file.xsd">
    <system>
        <section>
            <!-- Configuration section content goes here -->
        </section>
    </system>
</config>
```

Within each `<section>`, you can define multiple `<group>` elements, which further organize configuration fields.
Finally, within each `<group>`, you can define individual `<field>` elements to represent specific configuration
options.

## Defining Configuration Sections

Configuration sections group related settings together and provide a logical organization within the system.xml file.
Each `<section>` element must contain a unique `id` attribute to identify the section.

Here is an example of defining a configuration section named "General" with an associated group:

```xml
<section id="general" translate="label" type="text" sortOrder="10" showInDefault="1" showInWebsite="1" showInStore="1">
    <label>General Settings</label>
    <tab>my_custom_tab</tab>
    <resource>Vendor_Module::config_general</resource>
    <group id="general_group" sortOrder="10" showInDefault="1" showInWebsite="1" showInStore="1">
        <!-- Field definitions go here -->
    </group>
</section>
```

In the above example, we have specified various attributes for the `<section>` element:

- `id`: A unique identifier for the section.
- `translate`: A translation key for the section label.
- `type`: The type of section (e.g., text, number).
- `sortOrder`: The position of the section in relation to other sections.
- `showInDefault`, `showInWebsite`, and `showInStore`: Flags indicating whether the section should be visible in various
  configuration scopes (default, website, store).
- `label`: The label displayed for the section in the configuration UI.
- `tab`: The tab under which the section should be displayed in the configuration UI.
- `resource`: The ACL resource required to access the section.

## Adding Configuration Fields

Configuration fields represent specific settings within a section and are defined inside `<group>` elements.
Each `<field>` element must have a unique `id` attribute to identify the field.

Here is an example of defining a text field within a group:

```xml
<field id="my_text_field" translate="label" type="text" sort_order="10" show_in_default="1" show_in_website="1"
       show_in_store="1">
    <label>My Text Field</label>
    <comment>This is a sample text field.</comment>
    <backend_model>Vendor\Module\Model\Config\Backend\MyTextField</backend_model>
    <validate>validate-length maximum-length-255</validate>
</field>
```

In the above example, we have specified various attributes for the `<field>` element:

- `id`: A unique identifier for the field.
- `translate`: A translation key for the field label.
- `type`: The type of field (e.g., text, select, checkbox).
- `sort_order`: The position of the field in relation to other fields within the group.
- `show_in_default`, `show_in_website`, and `show_in_store`: Flags indicating whether the field should be visible in
  various configuration scopes (default, website, store).
- `label`: The label displayed for the field in the configuration UI.
- `comment`: Additional information or description for the field.
- `backend_model`: The backend model responsible for handling the field's value.
- `validate`: Validation rules to enforce on the field's value.

## Using Field Types

System.xml supports various field types to cater to different requirements. Some commonly used field types
include `text`, `select`, `checkbox`, `textarea`, and `multiselect`. Each field type has specific attributes and options
that can be set.

Here is an example of defining a select field:

```xml
<field id="my_select_field" translate="label" type="select" sort_order="20" show_in_default="1" show_in_website="1"
       show_in_store="1">
    <label>My Select Field</label>
    <source_model>Vendor\Module\Model\Config\Source\Options</source_model>
</field>
```

In the above example, the `source_model` attribute specifies a model that provides options for the select field. The
model should implement the `Magento\Framework\Option\ArrayInterface` interface to retrieve the available options.

## Validation and Sanitization

System.xml allows you to define validation rules for fields to ensure that the entered values meet specific criteria.
These rules are specified using the `<validate>` element within the `<field>` definition.

Here is an example of defining validation rules for a text field:

```xml
<field id="my_text_field" translate="label" type="text" sort_order="10" show_in_default="1" show_in_website="1"
       show_in_store="1">
    <label>My Text Field</label>
    <validate>validate-length maximum-length-255</validate>
</field>
```

In the above example, we have used the `validate-length` validation rule to enforce a maximum length of 255 characters
for the field's value.

## System.xml in Magento 2

In Magento 2, system.xml plays a vital role in configuring the behavior and appearance of modules. It allows merchants
to customize the settings of extensions and provides a user-friendly interface to manage these configurations.

By defining sections, groups, and fields in system.xml, you can create a comprehensive configuration interface for your
module, enabling users to modify settings according to their specific needs.

Magento 2 also provides various additional features and elements that can be combined with system.xml to enhance the
configuration experience, such as tabs, ACL resources, and scopes.

## Conclusion

System.xml is a powerful configuration file used in PHP and specifically in Magento 2 to define system-level settings
and configurations. This reference guide has provided an overview of the file's structure, syntax, and usage, along with
practical examples.

Understanding system.xml is essential for developing and customizing Magento 2 modules, as it allows you to define and
manage configuration options for your extensions. By leveraging the features and techniques discussed, you can create
flexible and user-friendly applications that meet the unique requirements of your clients.
