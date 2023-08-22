# `view.xml` Reference Documentation

[TOC]

The `view.xml` file is an important configuration file in Magento 2 that controls various visual aspects of the
frontend. This documentation will provide an in-depth explanation of the structure and options available in
the `view.xml` file, as well as how to customize it to meet your specific visual requirements.

## File Location

The `view.xml` file is typically located in the `app/design/frontend/<Vendor>/<Theme>/etc` directory of your Magento 2
installation. If the file does not exist, you can create it manually.

## Structure

The `view.xml` file follows an XML structure and is divided into several sections, each responsible for configuring a
specific visual aspect of the frontend. The main sections include `<vars>`, `<colors>`, `<images>`, `<templates>`,
and `<layout>`. Let's explore each section in detail.

### `<vars>`

The `<vars>` section allows you to define and override CSS variables. These variables can be used throughout your theme
to control various CSS properties. Here's an example of how to define a variable:

```xml
<vars module="Magento_Theme">
    <var name="customVariable">red</var>
</vars>
```

In this example, we define a variable named `customVariable` with the value `red`. This variable can then be used in
your CSS files like this:

```css
.my-element {
    background-color: var(--customVariable);
}
```

### `<colors>`

The `<colors>` section allows you to define and override color values used in your theme. You can specify colors for
various elements such as text, buttons, links, and more. Here's an example:

```xml
<colors>
    <color name="text.base">black</color>
    <color name="button.primary">blue</color>
</colors>
```

In this example, we set the base text color to `black` and the primary button color to `blue`. These color values can be
referenced in your CSS using the `@color` directive:

```css
.my-text {
    color: @color text . base;
}
```

### `<images>`

The `<images>` section is used to define image-related configuration. You can specify image sizes, aspect ratios, and
other properties. Here's an example:

```xml
<images module="Magento_Theme">
    <image id="product_page_main_image" type="image">
        <width>1000</width>
        <height>1000</height>
    </image>
</images>
```

In this example, we define an image with the id `product_page_main_image` and set its width and height to `1000`. This
configuration can be used in your theme's templates to control the size of the image.

### `<templates>`

The `<templates>` section allows you to define and override template files used in your theme. You can specify which
template files to use for different elements of the frontend. Here's an example:

```xml
<templates>
    <template id="Magento_Catalog::product/list.phtml">
        <overwrite>true</overwrite>
    </template>
</templates>
```

In this example, we specify that the template file `Magento_Catalog::product/list.phtml` should be used and overridden
in our theme. This allows you to customize the appearance and behavior of the product list page according to your
requirements.

### `<layout>`

The `<layout>` section defines the layout configuration for your theme. You can specify the layout files to use for
different pages and blocks. Here's an example:

```xml
<layout>
    <updates>
        <update id="my_custom_layout"/>
    </updates>
</layout>
```

In this example, we define a layout update with the id `my_custom_layout`. This layout update can be used to modify the
structure and arrangement of blocks on specific pages of your theme.

## Example

To illustrate how the `view.xml` file is used, let's take a specific example. Suppose you want to customize the
appearance of the product image on the product detail page. You can achieve this by modifying the `<images>` section of
your `view.xml` file:

```xml
<images module="Magento_Catalog">
    <image id="product_page_main_image" type="image">
        <width>800</width>
        <height>800</height>
    </image>
</images>
```

In this example, we set the width and height of the `product_page_main_image` to `800`, which will result in a larger
image size on the product detail page.

Remember to clear the cache after making changes to the `view.xml` file for the changes to take effect.

## Conclusion

The `view.xml` file is a powerful tool for customizing the visual aspects of your Magento 2 frontend. By understanding
its structure and options, you can tailor your theme to meet your specific design requirements. The examples provided in
this documentation should serve as a starting point for your customization efforts.
