# Widgets Documentation

[TOC]

## Introduction

Widgets are a powerful feature in Magento 2 that allow you to add dynamic content to your store's frontend without
writing code. In this documentation, we will go through the various aspects of using widgets in Magento 2, including
their configuration, customization, and usage. By the end, you will be able to leverage the full potential of widgets to
enhance the user experience of your Magento 2 store.

## What are Widgets?

Widgets in Magento 2 are reusable blocks of code that can be easily placed and managed on your store's frontend. They
provide a way to add dynamic content to your store without directly modifying the theme's files or writing complex code.

Widgets can be used to display product lists, banners, sliders, social media feeds, and more. They offer flexibility and
allow you to easily create engaging and personalized content for your customers.

## Widget Configuration

### Adding a Widget

To add a widget in Magento 2, follow these steps:

1. Log in to the Magento 2 Admin Panel.
2. Go to **Content** > **Elements** > **Widgets**.
3. Click on the **Add Widget** button.
4. Select the desired **Type** of widget, such as **Catalog Products List** or **CMS Static Block**.
5. Configure the widget settings based on your requirements. This may include selecting the target store view,
   specifying a container, and setting the layout updates.
6. Save the widget configuration.

### Widget Options

Each widget type in Magento 2 has its own set of configuration options. These options allow you to customize the
widget's behavior and appearance according to your needs. For example, a **Catalog Products List** widget may have
options to select the product category, set the number of products to display, and define the sorting order.

Widgets also provide layout update options, which allow you to position the widget in specific areas of your theme.
These areas can include the homepage, category pages, product pages, and more. By using layout updates, you have full
control over where and how the widget is displayed.

## Customizing Widgets

Magento 2 provides the ability to customize the appearance and functionality of widgets to align with your store's
branding and requirements. Some common customization options include:

### Widget Templates

Widget templates determine the HTML structure and styling of the widget. By default, Magento 2 offers a set of
predefined templates for each widget type. However, you can create custom templates to achieve a unique look and feel.

To create a custom widget template:

1. Copy the default template file from `vendor/magento-module-widget/view/frontend/templates/widget/` to your theme's
   folder.
2. Modify the copied template file according to your desired changes.

### Widget CSS Styles

You can also apply custom CSS styles to the widgets to match your store's branding. To do this, add CSS rules specific
to the widget's container or use the widget's unique class or ID.

For example, if you have a **CMS Static Block** widget with the ID `my-custom-block`, you can apply custom styles by
targeting the ID in your theme's CSS file:

```css
#my-custom-block {
    /* Add your custom styles here */
}
```

## Using Widgets

Once you have configured and customized your widgets, you can easily add them to your store's frontend.

### Using Widgets in CMS Pages and Blocks

To add a widget in a CMS page or block:

1. Edit the desired CMS page or block in the Magento 2 Admin Panel.
2. Place the cursor at the desired location where you want to add the widget.
3. Click on the **Insert Widget** button in the editor toolbar.
4. Select the widget you want to add from the list.
5. Configure the widget settings if required.
6. Save the CMS page or block.

### Using Widgets in Theme Layout Files

If you want to include a widget directly in your theme's layout XML files, you can do so by using the `<widget>` XML
tag.

For example, to include a **Catalog Products List** widget in the homepage, add the following code to your
theme's `cms_index_index.xml` layout file:

```xml
<container name="content.top">
    <referenceContainer name="content">
        <container name="widget.container" htmlTag="div" htmlClass="widget-container">
            <widget class="Magento\CatalogWidget\Block\Product\ProductsList"
                    template="Magento_CatalogWidget::product/widget/content/grid.phtml">
                <arguments>
                    <argument name="is_slider" xsi:type="boolean">true</argument>
                    <argument name="page_size" xsi:type="number">5</argument>
                    <argument name="template" xsi:type="string">
                        Magento_CatalogWidget::product/widget/content/grid.phtml
                    </argument>
                </arguments>
            </widget>
        </container>
    </referenceContainer>
</container>
```

## Conclusion

Widgets in Magento 2 provide a user-friendly and powerful way to add dynamic content to your store's frontend. By
following the steps outlined in this documentation, you can easily configure, customize, and use widgets to enhance the
user experience and drive more conversions on your Magento 2 store.
