# RequireJS Documentation

[TOC]

## Introduction

RequireJS is a JavaScript file and module loader that improves the efficiency and organization of code in web
applications. It allows you to break your code into small, modular pieces called modules and load them only when they
are needed, reducing the initial download time of your web page and improving the overall performance of your
application.

This documentation will provide a comprehensive guide to using RequireJS with a focus on integrating it with PHP and
Magento 2. We will cover the basic concepts of RequireJS, its configuration, and how to use it effectively in a Magento
2 environment.

## Installation

To get started with RequireJS, you can download it from the official website or include it via a package manager like
npm or Yarn. For Magento 2, RequireJS is already packaged and included in the installation.

You can include RequireJS in your HTML file by adding the following script tag:

```html

<script data-main="path/to/main.js" src="path/to/require.js"></script>
```

## Basic Concepts

### Modules

Modules are the building blocks of RequireJS. They encapsulate a piece of code, usually in a separate file, and expose
specific functionalities or data through a defined interface.

A module can be defined using the `define` function provided by RequireJS. It takes an array of dependencies and a
callback function that returns the module's exports.

```javascript
define(['dependency1', 'dependency2'], function (dep1, dep2) {
    // Module code here
    return {
        // Exports of the module
    };
});
```

### Dependencies

Dependencies are other modules that are required by a module to function correctly. RequireJS ensures that all
dependencies are loaded before executing the module code.

Dependencies are specified as an array of module names in the `define` function. The order of the dependencies is
important if the modules rely on each other.

```javascript
define(['dependency1', 'dependency2'], function (dep1, dep2) {
    // Module code here
});
```

### Asynchronous Module Definition (AMD)

RequireJS uses the Asynchronous Module Definition (AMD) format. This means that modules are loaded and executed
asynchronously, improving the performance of web applications.

AMD allows you to load modules on-demand, reducing the initial loading time of your application. It also provides a
clean and modular way to organize your code, making it easier to maintain and refactor.

## Configuring RequireJS

### RequireJS Configuration Object

RequireJS provides a configuration object that allows you to customize its behavior. You can specify module paths, shims
for non-AMD modules, and various other options.

The configuration object can be set using the `requirejs.config` method. It takes an object with configuration options
as its parameter.

```javascript
requirejs.config({
    // Configuration options here
});
```

### Configuration Example

Here's an example of how to configure RequireJS with custom module paths and shims:

```javascript
requirejs.config({
    baseUrl: 'js',
    paths: {
        'jquery': 'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min',
        'lodash': 'https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.21/lodash.min',
    },
    shim: {
        'jquery': {
            exports: '$'
        },
        'lodash': {
            exports: '_'
        }
    }
});
```

In this example, we set the base URL for all module paths to `'js'`, so RequireJS will look for modules in the `js`
directory. We also specify the paths for the `jquery` and `lodash` modules using CDN URLs.

The `shim` option is used to define exports for non-AMD modules. In this case, we specify that the `jquery` module
exports the global variable `$`, and the `lodash` module exports the global variable `_`.

## Using RequireJS in Magento 2

### Adding JavaScript Dependencies

Magento 2 uses RequireJS to manage JavaScript dependencies. To add new JavaScript dependencies to your Magento 2 module
or theme, you need to create a `requirejs-config.js` file.

In the `requirejs-config.js` file, you can specify the module name, its dependencies, and any other configuration
options.

Here's an example of how to add a JavaScript dependency to a Magento 2 theme:

```javascript
var config = {
    paths: {
        'my-custom-script': 'Vendor_Module/js/custom-script'
    }
};
```

In this example, we define a new module called `'my-custom-script'` and specify its path
as `'Vendor_Module/js/custom-script'`. This means that the module file `custom-script.js` should be located in
the `Vendor/Module/view/frontend/web/js` directory.

### Defining Custom Modules

To define custom modules in Magento 2, you can use the AMD format provided by RequireJS. Create a new JavaScript file
for your module and define it using the `define` function.

Here's an example of how to define a custom module in Magento 2:

```javascript
define(['jquery', 'lodash'], function ($, _) {
    // Module code here
});
```

In this example, we define a custom module that has `jquery` and `lodash` as dependencies. The module code can use
the `$` and `_` variables to access the functionality provided by jQuery and Lodash.

### Using RequireJS in Custom Magento 2 Themes

To load and use modules in a custom Magento 2 theme, you can use the `data-mage-init` attribute in HTML tags. This
attribute allows you to specify the module and its configuration options.

Here's an example of how to use RequireJS in a custom Magento 2 theme:

```html

<div data-mage-init='{"my-custom-script": {"option1": "value1", "option2": "value2"}}'>
    <!-- Content here -->
</div>
```

In this example, we use the `data-mage-init` attribute to initialize the `'my-custom-script'` module with the specified
configuration options. The module code will be executed for the specified HTML element.

## Conclusion

RequireJS is a powerful tool that enhances the performance and organization of JavaScript code in web applications. By
breaking code into modules and loading them asynchronously, you can improve the loading time of your web page and create
a more maintainable codebase.

In this documentation, we covered the basic concepts of RequireJS, its configuration options, and how to use it
effectively in a Magento 2 environment. By following the guidelines and examples provided, you should be able to
leverage RequireJS to enhance your PHP and Magento 2 projects.
