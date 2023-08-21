# `cron_jobs.xml` Reference Documentation

[TOC]

## Introduction

This reference documentation provides an in-depth explanation of the cron_jobs.xml file in Magento 2. Cron jobs are
scheduled tasks that are executed at predefined intervals. The cron_jobs.xml file allows you to configure and manage
these cron jobs in Magento 2.

## File Location and Structure

The cron_jobs.xml file is located in the `app/code/*Vendor*/*Module*/etc` folder of your Magento installation. It
follows the XML file format and defines the configuration for cron jobs.

Here is an example of the file structure:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Cron:etc/crontab.xsd">
    <group id="default">
        <job name="job_name" instance="*Vendor*\*Module*\Cron\*CronClass*" method="execute">
            <schedule>*schedule_expression*</schedule>
        </job>
    </group>
</config>
```

## File Components

The cron_jobs.xml file consists of the following components:

### 1. `config` Root Element

The `config` root element encloses the entire XML configuration. It includes the `xmlns:xsi` attribute, which specifies
the XML namespace for the `xsi` prefix, and the `xsi:noNamespaceSchemaLocation` attribute, which points to the cron jobs
XSD schema location.

### 2. `group` Element

The `group` element groups related cron jobs together. It has a required `id` attribute that identifies the group.

### 3. `job` Element

The `job` element defines a single cron job within a group. It has the following attributes:

- `name`: Specifies the unique name of the cron job.
- `instance`: Specifies the fully qualified class name of the cron job's implementation class.
- `method`: Specifies the method of the cron job's implementation class that should be executed.

### 4. `schedule` Element

The `schedule` element specifies the cron expression or schedule for the job. It defines when the cron job should be
executed. The `*schedule_expression*` should follow the cron syntax.

## Example

Let's consider an example to illustrate the usage of the cron_jobs.xml file. Assume we have a module
named `Vendor_Module` with a cron job that needs to run every hour.

1. Create the `cron_jobs.xml` file in the module's `etc` folder with the following content:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Cron:etc/crontab.xsd">
    <group id="default">
        <job name="vendor_module_cron" instance="Vendor\Module\Cron\MyCronClass" method="execute">
            <schedule>0 * * * *</schedule>
        </job>
    </group>
</config>
```

2. In the above example, the `group` element has an `id` attribute set to `default`. The `job` element has a `name`
   attribute set to `vendor_module_cron`, an `instance` attribute set to `Vendor\Module\Cron\MyCronClass`, and
   a `method` attribute set to `execute`. The `schedule` element specifies that the cron job should run every hour at
   the 0th minute.

3. In your PHP code, create the implementation class `MyCronClass` under `Vendor\Module\Cron`:

```php
<?php
namespace Vendor\Module\Cron;

class MyCronClass
{
    public function execute()
    {
        // Perform the required cron job tasks here
    }
}
```

4. With the above configuration and code, the `execute()` method of the `MyCronClass` class will be executed every hour.

## Conclusion

The cron_jobs.xml file allows you to configure and manage cron jobs in Magento 2. By following the structure and syntax
described in this documentation, you can define cron jobs and specify their schedules. Remember to provide the necessary
implementation class and method for each cron job.
 