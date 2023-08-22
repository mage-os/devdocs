# `email_templates.xml` Reference Documentation

[TOC]

This reference documentation provides detailed information on the structure and usage of the `email_templates.xml` file
in Magento 2. It is intended for developers familiar with PHP and Magento 2, and aims to provide authoritative and
knowledgeable guidance on creating and configuring email templates using XML.

## Introduction

The `email_templates.xml` file is an important configuration file used in Magento 2 to define email templates that can
be used for various email communications sent by the system. It allows developers to create customizable email templates
with dynamic content and configuration options.

This document provides a comprehensive guide on how to create, configure, and utilize email templates using
the `email_templates.xml` file in Magento 2.

## Structure of email_templates.xml

The `email_templates.xml` file follows a specific XML structure that defines the email templates and their associated
configurations. Here is a basic example of the structure:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Email:etc/email_templates.xsd">
    <template id="template_id" label="Template Label" file="file_name.html" type="html">
        <variables>
            <!-- Variable definitions -->
        </variables>
        <styles>
            <!-- CSS definitions -->
        </styles>
    </template>
</config>
```

The root `<config>` element contains the XML namespace declaration and the schema location for validation.
Inside `<config>`, there can be one or more `<template>` elements representing individual email templates.

Each `<template>` element requires the following attributes:

- `id`: A unique identifier for the template, typically in lowercase with underscores.
- `label`: A human-readable label or name for the template.
- `file`: The file name of the template HTML file (e.g., `file_name.html`).
- `type`: The content type of the template, typically `html` for HTML email templates.

## Creating Email Templates

To create a new email template, you need to add a `<template>` element inside the `<config>` element of
the `email_templates.xml` file. Here's an example:

```xml
<template id="custom_template" label="Custom Template" file="custom_template.html" type="html">
    <!-- Variable definitions and CSS styles go here -->
</template>
```

In the above example, we have defined a new email template with the ID `custom_template`, label `Custom Template`, and
associated HTML file `custom_template.html`.

## Using Variables

Email templates often require dynamic content, such as customer names, order details, or product information. Magento 2
provides a way to include variables in email templates to dynamically populate data.

To define variables for an email template, you need to add `<variable>` elements inside the `<variables>` section of
the `<template>` element. Here's an example:

```xml
<template id="custom_template" label="Custom Template" file="custom_template.html" type="html">
    <variables>
        <variable name="customer_name" xsi:type="string">John Doe</variable>
        <variable name="order_id" xsi:type="string">12345</variable>
    </variables>
    <!-- CSS styles and email content go here -->
</template>
```

In the above example, we have defined two variables: `customer_name` and `order_id`. These variables can be accessed
within the email template HTML file using the following syntax:

```html
<p>Dear {{var customer_name}},</p>
<p>Your order with ID {{var order_id}} has been processed.</p>
```

During email rendering, the variables will be replaced with their corresponding values.

## Configuring Templates

Apart from variable definitions, you can configure various aspects of an email template using the `<template>` element's
attributes. These attributes allow you to specify the subject, sender, and other settings for the email template.

Here's an example of configuring an email template:

```xml
<template id="custom_template" label="Custom Template" file="custom_template.html" type="html"
          subject="Custom Template Subject" sender_name="Store Name" sender_email="store@example.com">
    <!-- Variable definitions, CSS styles, and email content go here -->
</template>
```

In the above example, we have added the `subject`, `sender_name`, and `sender_email` attributes to the `<template>`
element. These attributes control the subject line, sender name, and sender email address for the email template.

## Advanced Configuration

The `email_templates.xml` file supports advanced configuration options to customize email headers, attachments, and
more. Here are a couple of examples:

### Adding Custom Headers

You can add custom headers to the email template by using the `<headers>` element inside the `<template>` element.
Here's an example:

```xml
<template id="custom_template" label="Custom Template" file="custom_template.html" type="html" ...>
<headers>
<header name="X-Custom-Header">Custom Value</header>
</headers>
        <!-- Variable definitions, CSS styles, and email content go here -->
        </template>
```

In the above example, we have added a custom header `X-Custom-Header` with the value `Custom Value` to the email
template.

### Adding Attachments

To include attachments in the email template, you can use the `<attachments>` element inside the `<template>` element.
Here's an example:

```xml
<template id="custom_template" label="Custom Template" file="custom_template.html" type="html" ...>
<attachments>
<attachment type="mimetype" encoding="encoding_type">attachment_content</attachment>
</attachments>
        <!-- Variable definitions, CSS styles, and email content go here -->
        </template>
```

In the above example, we have added an attachment with the specified `type`, `encoding`, and `attachment_content`.
Replace these values with the appropriate attachment details.

## Conclusion

The `email_templates.xml` file plays a crucial role in defining and configuring email templates in Magento 2. By
understanding its structure and utilizing its features, you can create customizable email templates with dynamic
content, variables, and advanced configuration options.

This reference documentation has provided you with a comprehensive understanding of `email_templates.xml` and equipped
you with the knowledge to create and configure email templates in Magento 2.
