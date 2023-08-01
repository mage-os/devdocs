# CSS Preprocessing Documentation

[TOC]

## Introduction

CSS preprocessing is a technique used to enhance the functionality and flexibility of CSS (Cascading Style Sheets). It
involves using a preprocessor to write CSS in a more dynamic and efficient manner. This documentation will provide an
overview of CSS preprocessing, explain its benefits, and discuss some popular CSS preprocessors such as Sass and Less.
Additionally, we will explore how CSS preprocessing can be utilized in PHP and Magento 2 environments.

## What is CSS Preprocessing?

CSS preprocessing is the process of writing CSS using a preprocessor, which is a tool that extends the capabilities of
CSS by adding features like variables, mixins, nesting, and more. These features allow developers to write CSS in a more
modular and reusable way, resulting in cleaner and more maintainable code.

Preprocessors work by taking input files written in a preprocessor language and transforming them into valid CSS files
that can be interpreted by browsers. This transformation is typically done using a command-line tool or a build system.

## Benefits of CSS Preprocessing

CSS preprocessing offers several key benefits for web developers:

### 1. Variables

CSS preprocessors allow the use of variables, which can be defined once and reused throughout the codebase. This makes
it easier to maintain consistency in styling, as changes to a variable value will be automatically reflected across all
instances.

Example:

```scss
$primary-color: #007bff;
.button {
  background-color: $primary-color;
}
```

### 2. Mixins

Mixins are reusable blocks of CSS code that can be included in multiple selectors. They allow developers to define
complex styles once and apply them wherever needed. This reduces code duplication and improves code organization.

Example:

```scss
@mixin button-styles {
  padding: 10px;
  background-color: $primary-color;
  color: white;
  border-radius: 5px;
}

.button {
  @include button-styles;
}

.submit-button {
  @include button-styles;
  background-color: green;
}
```

### 3. Nesting

CSS preprocessors support nesting, allowing developers to nest selectors inside other selectors. This makes the code
structure more intuitive and easier to read.

Example:

```scss
.container {
  background-color: #f1f1f1;

  .button {
    padding: 10px;
    background-color: $primary-color;
    color: white;
  }
}
```

### 4. Extending

Preprocessors support extending, which enables the inheritance of styles from one selector to another. This promotes
code reuse and reduces redundancy.

Example:

```scss
.button {
  padding: 10px;
  background-color: $primary-color;
  color: white;
}

.submit-button {
  @extend .button;
  background-color: green;
}
```

### 5. Modularity

CSS preprocessors allow developers to split their code into multiple files, making it easier to manage and organize
styles. These files can then be imported into a single master file, which will be compiled into a single CSS file by the
preprocessor.

Example:

```scss
// base.scss
$primary-color: #007bff;

.button {
  padding: 10px;
  background-color: $primary-color;
  color: white;
}

// main.scss
@import 'base';

.container {
  ...
}
```

## Popular CSS Preprocessors

There are several popular CSS preprocessors available, but two of the most widely used are Sass (Syntactically Awesome
Style Sheets) and Less. Both preprocessors offer similar features and are supported by a large community.

### Sass

Sass is a powerful and mature CSS preprocessor that provides a wide range of features. It has a large and active
community, making it easy to find resources and support. Sass supports two syntaxes: SCSS (Sassy CSS), which is a
superset of CSS, and the indented syntax.

To compile Sass files into CSS, you can use the command line or build tools like Grunt, Gulp, or Webpack.

Example of SCSS syntax:

```scss
$primary-color: #007bff;

.button {
  padding: 10px;
  background-color: $primary-color;
  color: white;
}
```

Example of indented syntax:

```sass
$primary-color: #007bff

.button
  padding: 10px
  background-color: $primary-color
  color: white
```

### Less

Less is another popular CSS preprocessor that provides similar features to Sass. It has a more concise syntax compared
to Sass, resembling traditional CSS. Less also has a large community and can be compiled using command-line tools or
build systems.

Example:

```less
@primary-color: #007bff;

.button {
  padding: 10px;
  background-color: @primary-color;
  color: white;
}
```

## Using CSS Preprocessing in PHP and Magento 2

CSS preprocessing can be integrated into PHP and Magento 2 projects to enhance the styling capabilities. To utilize CSS
preprocessors in these environments, additional setup steps are required.

1. **PHP**: To use CSS preprocessing in PHP projects, you need to set up a build system or task runner like Grunt, Gulp,
   or Webpack. These tools can be configured to watch and compile your preprocessor files into CSS whenever changes are
   made. The compiled CSS files can then be included in your PHP files as usual.

2. **Magento 2**: Magento 2 utilizes the LESS preprocessor by default for its frontend styles. To customize and extend
   styles in Magento 2, you can create a custom theme and override the default LESS files. This allows you to leverage
   the power of LESS and its preprocessing features within the Magento 2 framework.

Example of overriding a LESS file in a Magento 2 custom theme:

```
app/design/frontend/MyVendor/my-theme/web/css/source/_extend.less
```

```less
@primary-color: #007bff;

.button {
  padding: 10px;
  background-color: @primary-color;
  color: white;
}
```

## Conclusion

CSS preprocessing is a powerful technique that enhances the capabilities of CSS by introducing features like variables,
mixins, nesting, and more. By using CSS preprocessors like Sass or Less, developers can write cleaner and more
maintainable code. In PHP and Magento 2 environments, CSS preprocessing can be integrated with build systems or custom
themes to unlock the full potential of CSS preprocessing. Experiment with CSS preprocessors and experience the benefits
of improved organization, modularity, and code reusability in your projects.
