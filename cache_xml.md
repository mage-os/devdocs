# `cache.xml` Reference Documentation

[TOC]

## Introduction

The cache.xml file is an essential configuration file in Magento 2 that controls the caching behavior of your
application. By properly configuring this file, you can optimize the caching process, improve performance, and enhance
the overall user experience of your Magento 2 website.

In this reference documentation, we will explore the structure and key elements of the cache.xml file. We will provide
you with concrete examples and code snippets to help you understand and leverage the power of cache.xml in your Magento
2 projects.

## Understanding the Structure

The cache.xml file is located in the `app/etc/` directory of your Magento 2 installation. It follows a hierarchical
structure with a root `<config>` element, which contains multiple `<type>` elements representing different cache types.

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Cache/etc/cache.xsd">
    <type name="cache_type1"/>
    <type name="cache_type2"/>
    ...
</config>
```

Each `<type>` element represents a cache type that can be enabled or disabled individually. Magento 2 provides several
predefined cache types, such as `config`, `layout`, `block_html`, and `full_page`, among others. Additionally, you can
create custom cache types to suit your specific needs.

## Configuring Cache Types

To optimize caching for your Magento 2 application, you can configure each cache type by adding child elements within
the corresponding `<type>` element. These child elements define various properties and behaviors for each cache type.

### Example: Configuring the `config` Cache Type

```xml
<type name="config">
    <backend_model>Magento\Framework\Cache\Backend\File</backend_model>
    <backend_model>Magento\Framework\App\Cache\StateInterface</backend_model>
    <config_model>Magento\Framework\App\Cache\Config</config_model>
    <cache_dir>cache_dir/config</cache_dir>
    <description>Configuration files cache</description>
</type>
```

In the example above, we configure the `config` cache type. Let's understand the purpose of each child element:

- `<backend_model>`: Specifies the backend model responsible for storing and retrieving cached data. In this case,
  both `Magento\Framework\Cache\Backend\File` and `Magento\Framework\App\Cache\StateInterface` are used.
- `<config_model>`: Defines the configuration model responsible for managing the cache type. In this
  example, `Magento\Framework\App\Cache\Config` is used.
- `<cache_dir>`: Specifies the directory where the cached data will be stored. The value `cache_dir/config` sets the
  cache directory for the `config` cache type.
- `<description>`: Provides a brief description of the cache type, which can be helpful for documentation or debugging
  purposes.

You can configure other cache types in a similar manner, adjusting the specific elements and values according to your
requirements.

## Enabling and Disabling Cache Types

By default, all cache types are enabled in Magento 2. However, you may choose to disable specific cache types that are
not necessary for your particular application. Disabling cache types can help reduce the amount of data stored in the
cache and improve performance.

To enable or disable a cache type, you can modify the `<type>` element in the cache.xml file. Set the `enabled`
attribute to either `true` or `false` to enable or disable the cache type, respectively.

### Example: Disabling the `block_html` Cache Type

```xml
<type name="block_html" enabled="false"/>
```

In the example above, the `block_html` cache type is disabled by setting the `enabled` attribute to `false`. This can be
useful during development or debugging stages, where you frequently modify layout or block templates.

Remember to clear the cache after enabling or disabling cache types to ensure the changes take effect.

## Conclusion

The cache.xml file is a pivotal configuration file in Magento 2 that allows you to control the caching behavior of your
application. By understanding its structure and utilizing the available elements, you can optimize caching, improve
performance, and deliver a seamless user experience.

In this reference documentation, we explored the structure of cache.xml, learned how to configure cache types, and
discovered how to enable or disable them. We provided you with concrete examples and code snippets to help you apply
these concepts in your Magento 2 projects.

Now armed with this knowledge, you can harness the power of cache.xml to unleash the full potential of caching in your
Magento 2 applications. Happy coding!
