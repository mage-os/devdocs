# ACL XML Reference Documentation

This reference documentation provides information on the structure and usage of the acl.xml file in Magento 2. acl.xml is an essential configuration file used to define Access Control List (ACL) permissions for various resources in your Magento 2 module or extension.

## 1. Introduction

Access Control List (ACL) is a security mechanism used to control access to resources based on user roles and permissions. The acl.xml file is used in Magento 2 to define these roles, resources, and associated permissions for your module or extension.

## 2. Structure of acl.xml

The acl.xml file follows a specific structure and should be placed in the `etc` directory of your module or extension. Here is an example of the basic structure of acl.xml:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Acl/etc/acl.xsd">
    <acl>
        <!-- Define resources and roles here -->
    </acl>
</config>
```

The `xmlns:xsi` and `xsi:noNamespaceSchemaLocation` attributes define the XML schema for validation. The `<acl>` tag is the root element, under which you define resources and roles.

## 3. Defining Resources and Roles

In the `<acl>` tag, you define `<resources>` and `<role>` elements to specify the resources and roles respectively. A resource represents a specific functionality or area in your module or extension, while a role represents a user role or group.

Here is an example of defining a resource and a role in acl.xml:

```xml
<config>
    <acl>
        <resources>
            <resource id="Namespace_Module::resource_id" title="Resource Title" sortOrder="10">
                <!-- Define child resources here -->
            </resource>
        </resources>
        
        <roles>
            <role id="Namespace_Module::role_id" title="Role Title" sortOrder="10">
                <!-- Define role's allowed resources here -->
            </role>
        </roles>
    </acl>
</config>
```

In the above example, the `<resource>` element defines a resource with an `id`, `title`, and `sortOrder`. The `id` should follow the format `<Namespace_Module>::<resource_id>`. Similarly, the `<role>` element defines a role with an `id`, `title`, and `sortOrder`.

## 4. Applying ACL Permissions

Once you have defined resources and roles, you need to specify the permissions or access rules for each role on the respective resources. For this, you use the `<resource>` and `<permission>` elements.

Here is an example of applying ACL permissions in acl.xml:

```xml
<config>
    <acl>
        <resources>
            <resource id="Namespace_Module::resource_id" title="Resource Title" sortOrder="10">
                <resource id="Namespace_Module::child_resource_id" title="Child Resource Title" sortOrder="10">
                    <permission id="Namespace_Module::permission_id" title="Permission Title" sortOrder="10"/>
                </resource>
            </resource>
        </resources>
        
        <roles>
            <role id="Namespace_Module::role_id" title="Role Title" sortOrder="10">
                <resource id="Namespace_Module::resource_id" title="Resource Title">
                    <resource id="Namespace_Module::child_resource_id" title="Child Resource Title">
                        <permission id="Namespace_Module::permission_id" title="Permission Title" />
                    </resource>
                </resource>
            </role>
        </roles>
    </acl>
</config>
```

In the above example, the `<permission>` element is nested under the appropriate `<resource>` and `<role>`. The `id` attribute follows the format `<Namespace_Module>::<permission_id>`. The `title` attribute provides a human-readable title for the permission.

## 5. Examples

Here are a few examples to illustrate how to define resources, roles, and apply ACL permissions in acl.xml:

### Example 1: Defining a Resource

```xml
<resources>
    <resource id="Namespace_Module::resource_id" title="Resource Title" sortOrder="10">
        <!-- Define child resources here -->
    </resource>
</resources>
```

### Example 2: Defining a Role

```xml
<roles>
    <role id="Namespace_Module::role_id" title="Role Title" sortOrder="10">
        <!-- Define role's allowed resources here -->
    </role>
</roles>
```

### Example 3: Applying Permissions to a Role

```xml
<roles>
    <role id="Namespace_Module::role_id" title="Role Title" sortOrder="10">
        <resource id="Namespace_Module::resource_id" title="Resource Title">
            <resource id="Namespace_Module::child_resource_id" title="Child Resource Title">
                <permission id="Namespace_Module::permission_id" title="Permission Title" />
            </resource>
        </resource>
    </role>
</roles>
```

## Conclusion

The acl.xml file is a crucial configuration file in Magento 2 for defining Access Control List (ACL) permissions. By understanding its structure and usage, you can control access to resources based on user roles and permissions effectively.
