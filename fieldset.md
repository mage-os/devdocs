# Fieldset.xml Reference Documentation

## Introduction

The `fieldset.xml` file is an important configuration file in the Magento 2 framework. It is used to define and modify
the structure of data fields retrieved from database tables and models. This documentation will guide you through the
different elements and attributes used in `fieldset.xml` and their corresponding functionalities. By understanding and
correctly using `fieldset.xml`, you can customize and extend the data fields in your Magento 2 application.

## File Structure

The `fieldset.xml` file follows a specific structure that consists of one or more `<fieldset>` elements.
Each `<fieldset>` element can contain one or more `<container>` elements, and each `<container>` element can contain one
or more `<field>` elements. Here is an example of the basic structure of a `fieldset.xml` file:

```xml
<fieldset>
    <container name="container_name">
        <field name="field_name" sortOrder="sort_order" component="component_name"/>
    </container>
</fieldset>
```

Throughout this documentation, we will examine each element and attribute in detail, providing examples and code
snippets to illustrate their usage.

## Element: fieldset

The `<fieldset>` element is the root element of the `fieldset.xml` file. It is used to define a group of data fields.
Each `fieldset.xml` file can contain multiple `<fieldset>` elements. Here is an example of a `fieldset.xml` file with
multiple `<fieldset>` elements:

```xml
<fieldset>
    <!-- First fieldset definition -->
</fieldset>

<fieldset>
<!-- Second fieldset definition -->
</fieldset>
```

## Element: container

The `<container>` element is used to group related fields together within a `<fieldset>`. It provides a way to organize
and structure the fields. Each `<container>` element can contain one or more `<field>` elements. Here is an example of
a `fieldset.xml` file with a `<container>` element:

```xml
<fieldset>
    <container name="billing_information">
        <field name="first_name" sortOrder="10" component="Magento_Ui/js/form/element/abstract"/>
        <field name="last_name" sortOrder="20" component="Magento_Ui/js/form/element/abstract"/>
    </container>
</fieldset>
```

## Element: field

The `<field>` element is used to define a data field within a `<container>`. It specifies the name, sort order, and
component of the field. The name attribute is mandatory, while the sortOrder and component attributes are optional. Here
is an example of a `fieldset.xml` file with a `<field>` element:

```xml
<fieldset>
    <container name="billing_information">
        <field name="first_name" sortOrder="10" component="Magento_Ui/js/form/element/abstract"/>
    </container>
</fieldset>
```

## Attribute: name

The `name` attribute is used to specify the name of a `<container>` or `<field>`. It serves as a unique identifier for
the container or field within the `fieldset.xml` file. The name should be a string without spaces or special characters.
For example, a field with the name "first_name" can be defined as follows:

```xml
<fieldset>
    <container name="billing_information">
        <field name="first_name" sortOrder="10" component="Magento_Ui/js/form/element/abstract"/>
    </container>
</fieldset>
```

## Attribute: sortOrder

The `sortOrder` attribute is used to specify the order in which fields are rendered within a `<container>`. Fields with
lower `sortOrder` values will be rendered before fields with higher `sortOrder` values. The `sortOrder` attribute is
optional, and if not specified, fields will be rendered in the order they are defined in the `fieldset.xml` file. Here
is an example of a `fieldset.xml` file with fields sorted using the `sortOrder` attribute:

```xml
<fieldset>
    <container name="billing_information">
        <field name="first_name" sortOrder="10" component="Magento_Ui/js/form/element/abstract"/>
        <field name="last_name" sortOrder="20" component="Magento_Ui/js/form/element/abstract"/>
    </container>
</fieldset>
```

## Attribute: component

The `component` attribute is used to specify the JavaScript component that will render the field in the user interface.
The component determines the behavior and appearance of the field. The value of the `component` attribute should be a
valid JavaScript component path. Here is an example of a `fieldset.xml` file with a field component specified:

```xml
<fieldset>
    <container name="billing_information">
        <field name="first_name" sortOrder="10" component="Magento_Ui/js/form/element/abstract"/>
    </container>
</fieldset>
```

## Example Usage

To illustrate the usage of `fieldset.xml`, let's consider an example where we want to add a custom field named "age" to
the "customer_account_edit" form. We can achieve this by creating a `fieldset.xml` file in our custom module with the
following content:

```xml
<fieldset>
    <container name="customer">
        <field name="age" sortOrder="70" component="Magento_Ui/js/form/element/input"/>
    </container>
</fieldset>
```

After creating the `fieldset.xml` file, we need to declare it in the module's `di.xml` file as follows:

```xml
<type name="Magento\Customer\Block\Form\Edit">
    <arguments>
        <argument name="formCode" xsi:type="const">\Magento\Customer\Block\Form::FORM_CODE_EDIT</argument>
        <argument name="data" xsi:type="array">
            <item name="fieldsetForm" xsi:type="array">
                <item name="config" xsi:type="array">
                    <item name="dataScope" xsi:type="string">data</item>
                    <item name="additionalClasses" xsi:type="string">admin__fieldset-form</item>
                    <item name="namespace" xsi:type="string">fieldset_form</item>
                </item>
                <item name="children" xsi:type="array">
                    <item name="customer" xsi:type="array">
                        <item name="children" xsi:type="array">
                            <item name="age" xsi:type="array">
                                <item name="sortOrder" xsi:type="number">70</item>
                                <item name="dataScope" xsi:type="string">age</item>
                                <item name="label" xsi:type="string" translate="true">Age</item>
                                <item name="component" xsi:type="string">Magento_Ui/js/form/element/input</item>
                            </item>
                        </item>
                    </item>
                </item>
            </item>
        </argument>
    </arguments>
</type>
```

In this example, the `<container>` element is named "customer", and it contains a single `<field>` element with the
name "age". The "age" field is rendered using the "Magento_Ui/js/form/element/input" JavaScript component.

By following the above steps, the "age" field will be added to the customer account edit form in the Magento 2 backend.

## Conclusion

`fieldset.xml` is a powerful configuration file in Magento 2 that allows you to customize and extend the data fields in
your application. By understanding the elements and attributes in `fieldset.xml`, you can control the structure and
behavior of your data fields.
