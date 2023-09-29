# Theme Development Documentation

[TOC]

## Introduction

This documentation provides a comprehensive guide to theme development in Magento 2. It covers the essential concepts,
techniques, and best practices required to create custom themes for Magento 2 stores.

Please note that this documentation assumes a familiarity with programming concepts, particularly PHP and Magento 2. If
you are new to Magento 2 or programming, it is recommended to familiarize yourself with these topics before proceeding
further.

## Theme Anatomy

Before diving into theme development, it is essential to understand the structure and components of a Magento 2 theme. A
theme consists of the following main elements:

1. **Theme Files**: These include layout XML files, template files (`.phtml`), CSS files, JavaScript files, and other
   assets.
2. **Theme Configuration**: Magento 2 uses XML configuration files to define theme-specific settings, such as logo,
   colors, and fonts.
3. **Theme Inheritance**: Themes can inherit from other themes, allowing for customization and extension of existing
   themes.
4. **Theme Layouts**: Layout XML files control the structure and composition of pages in a Magento 2 store.
5. **Theme Templates**: Template files define the HTML structure and content of various components in a theme.
6. **Theme CSS and JavaScript**: CSS and JavaScript files control the appearance and behavior of a theme.
7. **Theme Deployment**: Themes need to be deployed to make them available to a Magento 2 store.

## Creating a Custom Theme

To create a custom theme in Magento 2, follow these steps:

1. Create a new directory for your theme under `app/design/frontend/{Vendor}/{theme}`. For example, if your theme is
   called "MyTheme" and your vendor is "Acme", the path would be `app/design/frontend/Acme/MyTheme`.
2. Create a `theme.xml` file within your theme's directory. This file defines the theme's name, parent theme, and other
   configuration options. Here's an example:

```xml
<theme xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="urn:magento:framework:Config/etc/theme.xsd">
    <title>MyTheme</title>
    <parent>Magento/blank</parent>
</theme>
```

3. Create a `registration.php` file in your theme's directory. This file registers your theme and makes it available to
   Magento 2. Here's an example:

```php
<?php

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::THEME,
    'frontend/Acme/MyTheme',
    __DIR__
);
```

4. To load the new theme, run the command `bin/magento setup:upgrade`.

Your custom theme is now ready to be customized and extended as per your requirements.

## Define a Preview Image (Optional)

You can specify a preview image for your theme using the following XML configuration in your `theme.xml`:

```xml
<theme xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="urn:magento:framework:Config/etc/theme.xsd">
    <title>MyTheme</title>
    <parent>Magento/blank</parent>
    <media>
        <preview_image>media/preview.jpg</preview_image>
    </media>
</theme>
```

Ensure that the specified image file exists in your theme directory. If it doesn't, running `bin/magento setup:upgrade` will produce an error:

```
File "app/design/frontend/Acme/MyTheme/media/preview.jpg" does not exist.
```

## Theme Inheritance

Magento 2 supports theme inheritance, allowing you to extend and customize existing themes. This reduces duplication and
makes it easier to maintain themes. To inherit from a parent theme, specify it in the `theme.xml` file of your custom
theme using the `<parent>` tag. Here's an example:

```xml
<parent>Magento/luma</parent>
```

By inheriting from a parent theme, you can override specific files, add new files, and modify theme settings to achieve
the desired customization.

## Theme Layouts

Layouts in Magento 2 define the structure and composition of pages. A layout is defined using XML files located in
the `app/design/frontend/{Vendor}/{theme}/Magento_Theme/layout` directory. Each layout file controls a specific page or
block within a page. For example, the `default.xml` file controls the structure of the entire store, while
the `cms_index_index.xml` file controls the homepage layout.

Layout files consist of blocks, containers, and references, which define the structure of a page. Blocks represent
individual components, such as header, footer, and sidebar, while containers act as placeholders for blocks. References
are used to specify the location of blocks within containers.

Here's an example of a simple layout XML file that adds a block to the homepage:

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" layout="1column"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="content">
            <block class="Magento\Framework\View\Element\Template" name="custom.block"
                   template="Magento_Theme::custom_template.phtml"/>
        </referenceContainer>
    </body>
</page>
```

This example adds a block named "custom.block" to the "content" container. The block uses the template
file `custom_template.phtml` from the `Magento_Theme` module.

You can create and customize layout XML files within your theme to control the structure of various pages in your
Magento 2 store.

## Theme Templates

Template files in Magento 2 define the HTML structure and content of various components within a theme. The template
files have the extension `.phtml` and are located in the `app/design/frontend/{Vendor}/{theme}/Magento_Theme/templates`
directory.

To customize a particular component, you can override its template file in your custom theme. For example, to override
the header template, create a file called `header.phtml` within your theme's template directory and modify it as per
your requirements.

You can also use template files to display dynamic data or perform complex logic by using PHP code. However, it is
recommended to keep the logic to a minimum and separate it from the presentation using blocks, which we will discuss in
the next section.

## Theme CSS and JavaScript

CSS and JavaScript files control the appearance and behavior of a theme. In Magento 2, these files are located in
the `app/design/frontend/{Vendor}/{theme}/web` directory.

To add custom CSS or JavaScript to your theme, create a directory structure within the `web` directory that mirrors the
file structure you want to override. For example, to override the default CSS file of a theme, create a file
called `styles.css` within the `css` directory of your custom theme.

You can also add new CSS or JavaScript files and reference them in your layout XML files. This allows for greater
flexibility in customizing and extending the behavior of your theme.

## Overriding Core Theme Files

Magento 2 allows you to override core theme files without modifying the original files. By placing a file with the same
name and location in your custom theme, Magento 2 will prioritize the file from your custom theme over the core file.

For example, to override the default header template (`header.phtml`), create a file with the same name and location in
your custom theme: `app/design/frontend/{Vendor}/{theme}/Magento_Theme/templates/html/header.phtml`. Any modifications
made to this file will be reflected in your store, without touching the original core file.

This approach ensures that your customizations remain separate from the core codebase, making it easier to upgrade
Magento 2 in the future.

## Theme Configuration

Magento 2 allows you to configure various theme settings, such as logo, colors, fonts, etc., using theme configuration
files. These files are located in the `app/design/frontend/{Vendor}/{theme}/etc` directory.

To configure your theme, create a file called `view.xml` within your theme's `etc` directory. This file defines various
settings, such as image sizes, color swatches, and other visual aspects of your theme. Here's an example:

```xml
<view xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:Config/etc/view.xsd">
    <media>
        <images module="Magento_Catalog">
            <image id="category_page_grid" type="small_image">
                <width>240</width>
                <height>300</height>
            </image>
        </images>
    </media>
</view>
```

This example defines the dimensions for the category page grid image. You can customize this file to configure various
aspects of your theme as per your requirements.

## Theme Deployment

Once you have developed and customized your theme, it needs to be deployed to make it available to your Magento 2 store.
Magento 2 provides a set of commands to deploy themes and other assets.

To deploy your theme, run the following command from your Magento 2 root directory:

```bash
bin/magento setup:static-content:deploy
```

This command generates static files for all enabled themes, including your custom theme, and places them in the
appropriate directories to be served by the web server.

After the deployment, your custom theme will be available for selection in the Magento 2 admin panel under **Content >
Design > Configuration**.

## Conclusion

This documentation has covered the fundamental concepts and techniques required for theme development in Magento 2. By
understanding the theme anatomy, creating custom themes, leveraging theme inheritance, working with layouts, templates,
CSS, JavaScript, and overriding core theme files, you can create visually appealing and customized themes for your
Magento 2 store.

Remember to adhere to best practices, maintain separation between custom and core code, and regularly test your themes
to ensure compatibility and performance. With these skills and knowledge, you are well-equipped to build stunning and
engaging themes in Magento 2.
