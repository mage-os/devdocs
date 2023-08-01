# JavaScript in Magento 2 Documentation

[TOC]

## Introduction

Magento 2 is a powerful e-commerce platform that supports the use of JavaScript to enhance the user experience and add
dynamic functionality to your storefront. This documentation provides a comprehensive guide to JavaScript in Magento 2,
covering important concepts, best practices, and examples.

## JavaScript Libraries in Magento 2

Magento 2 leverages several popular JavaScript libraries to facilitate development and provide a robust set of tools and
features. The key libraries used in Magento 2 include:

- [jQuery](https://jquery.com/): A fast and compact JavaScript library that simplifies HTML document traversing, event
  handling, and Ajax interactions.
- [RequireJS](https://requirejs.org/): A JavaScript file and module loader that allows modular development and optimizes
  resource loading.
- [KnockoutJS](https://knockoutjs.com/): A JavaScript library that enables the creation of responsive and dynamic user
  interfaces with a clean and flexible MVVM architecture.
- [Magento_Ui](https://devdocs.magento.com/guides/v2.4/javascript-dev-guide/javascript/js-coding-standard.html): A
  Magento 2-specific JavaScript library that provides reusable UI components and widgets.

## Using JavaScript in Magento 2

Magento 2 offers various ways to include and utilize JavaScript in your modules or themes. Here are a few key methods:

### Adding JavaScript to Pages

You can add JavaScript to specific pages by declaring dependencies in the `requirejs-config.js` file of your module or
theme. Here's an example that adds a custom JavaScript file to a specific page:

```javascript
// app/code/YourVendor/YourModule/view/frontend/requirejs-config.js

var config = {
    map: {
        '*': {
            'your-custom-js': 'YourVendor_YourModule/js/your-custom-js',
        }
    }
};
```

In the above example, 'your-custom-js' is the name of your custom JavaScript file, and '
YourVendor_YourModule/js/your-custom-js' is the path to the JavaScript file relative to your module or theme.

### Using UI Components

Magento 2 provides UI components that encapsulate JavaScript functionality and can be easily integrated into your
modules or themes. You can create custom UI components or extend existing ones to meet your specific requirements.
Here's an example of adding a custom UI component to a template file:

```html
<!-- app/code/YourVendor/YourModule/view/frontend/web/template/custom-component.html -->

<div data-bind="scope: 'customScope'">
    <!-- Your UI component markup here -->
</div>

<script type="text/x-magento-init">
{
    "*": {
        "Magento_Ui/js/core/app": {
            "components": {
                "customScope": {
                    "component": "YourVendor_YourModule/js/custom-component"
                }
            }
        }
    }
}

</script>
```

In this example, 'custom-component.html' is the template file for your custom UI component, and '
YourVendor_YourModule/js/custom-component' is the JavaScript file that defines the behavior of your UI component.

## JavaScript Best Practices in Magento 2

To ensure efficient and maintainable JavaScript code, it is important to follow best practices when developing in
Magento 2. Here are some key considerations:

### Use RequireJS for Module Loading

Magento 2 utilizes RequireJS for module loading. When developing custom JavaScript modules, make sure to define
dependencies properly and use the `define` function to encapsulate module functionality. This ensures proper ordering of
script loading and avoids conflicts.

### Leverage KnockoutJS for UI Interactions

KnockoutJS is the recommended library for handling user interactions and updating UI components in Magento 2. Use
KnockoutJS observables and bindings to create responsive and dynamic user interfaces.

### Minimize DOM Manipulation

Excessive DOM manipulation can degrade performance. Instead, make use of KnockoutJS bindings and the Magento 2 UI
component system to update UI elements efficiently.

### Follow Magento 2 JavaScript Coding Standards

Magento 2 has specific coding standards for JavaScript. Adhering to these standards ensures consistency and readability
across your codebase. Familiarize yourself with the Magento 2 JavaScript coding standards described in the official
documentation.

## Code Examples

Let's conclude this documentation with a few code examples that illustrate the concepts discussed above. Refer to these
examples for practical implementation guidance:

- [Example 1: Adding a Custom JavaScript File to a Page](#example-1-adding-a-custom-javascript-file-to-a-page)
- [Example 2: Creating a Custom UI Component](#example-2-creating-a-custom-ui-component)

### Example 1: Adding a Custom JavaScript File to a Page

To add a custom JavaScript file to a specific page, follow these steps:

1. Create the JavaScript file at the desired location (
   e.g., `app/code/YourVendor/YourModule/view/frontend/web/js/your-custom-js.js`).

2. Declare the JavaScript file as a dependency in the `requirejs-config.js` file of your module or theme:

```javascript
// app/code/YourVendor/YourModule/view/frontend/requirejs-config.js

var config = {
    map: {
        '*': {
            'your-custom-js': 'YourVendor_YourModule/js/your-custom-js',
        }
    }
};
```

3. Use the JavaScript file in your page by adding the following code to the corresponding template file:

```html
<!-- app/code/YourVendor/YourModule/view/frontend/templates/custom-page.phtml -->

<script>
    require(['your-custom-js'], function () {
        // Your JavaScript code here
    });
</script>
```

### Example 2: Creating a Custom UI Component

To create a custom UI component in Magento 2, follow these steps:

1. Create the UI component template file (
   e.g., `app/code/YourVendor/YourModule/view/frontend/web/template/custom-component.html`) and define the UI component
   markup.

2. Create the JavaScript file that defines the behavior of the UI component (
   e.g., `app/code/YourVendor/YourModule/view/frontend/web/js/custom-component.js`).

3. In the template file where you want to use the custom UI component, add the following code:

```html
<!-- app/code/YourVendor/YourModule/view/frontend/templates/custom-template.phtml -->

<div data-bind="scope: 'customScope'">
    <!-- Your UI component markup here -->
</div>

<script type="text/x-magento-init">
{
    "*": {
        "Magento_Ui/js/core/app": {
            "components": {
                "customScope": {
                    "component": "YourVendor_YourModule/js/custom-component"
                }
            }
        }
    }
}

</script>
```

These code examples should help you understand the practical implementation of JavaScript in Magento 2.

## Conclusion

This documentation has provided a comprehensive guide to JavaScript in Magento 2, covering important concepts, best
practices, and practical examples. By leveraging JavaScript libraries, utilizing various methods of including
JavaScript, and following best practices, you can enhance the functionality and user experience of your Magento 2
storefront. Happy coding!
