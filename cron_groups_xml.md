# `cron_groups.xml` Reference Documentation

[TOC]

## Overview

The `cron_groups.xml` file is a configuration file used in Magento 2 to define cron groups and their associated cron
jobs. Cron jobs are scheduled tasks that are executed automatically at specified intervals. Cron groups allow you to
categorize and manage cron jobs more effectively.

This reference documentation will provide you with a detailed explanation of the `cron_groups.xml` file and its
structure. It will also cover the various elements and attributes used in this file, along with their purpose and usage.

## File Location

The `cron_groups.xml` file is located in the `<module_dir>/etc` directory of your Magento 2 module. It follows the `XML`
file format and can be edited using any text editor or integrated development environment (IDE) of your choice.

## File Structure

The `cron_groups.xml` file follows a specific structure that consists of several XML elements and attributes. Here is an
example of the basic structure:

```xml
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Cron:etc/cron_groups.xsd">
    <group id="default">
        <schedule_generate_every>1</schedule_generate_every>
        <schedule_ahead_for>4</schedule_ahead_for>
        <schedule_lifetime>2</schedule_lifetime>
        <history_cleanup_every>10</history_cleanup_every>
        <history_success_lifetime>60</history_success_lifetime>
        <history_failure_lifetime>600</history_failure_lifetime>
        <use_separate_process>0</use_separate_process>
    </group>
    <!-- Additional cron groups and their configurations -->
</config>
```

The root element of the file is `<config>`, which contains several child elements representing cron groups. Each cron
group is defined within a `<group>` element, with a unique `id` attribute identifying it. The various configurations for
each cron group are specified as child elements within the `<group>` element.

## Elements and Attributes

### `<group>`

The `<group>` element represents a cron group and contains various child elements for configuring the group. It has the
following attribute:

- `id` (required): Specifies a unique identifier for the cron group. This identifier is referenced in other
  configuration files to assign cron jobs to this group.

Example:

```xml
<group id="default">
    <!-- Group configurations -->
</group>
```

### `<schedule_generate_every>`

The `<schedule_generate_every>` element determines how often the cron schedule is regenerated. It sets the frequency in
minutes for generating the cron schedule.

Example:

```xml
<schedule_generate_every>1</schedule_generate_every>
```

### `<schedule_ahead_for>`

The `<schedule_ahead_for>` element specifies the number of minutes ahead of the current time for which the cron schedule
is generated. It helps in ensuring that scheduled tasks are executed on time by allowing a buffer for processing.

Example:

```xml
<schedule_ahead_for>4</schedule_ahead_for>
```

### `<schedule_lifetime>`

The `<schedule_lifetime>` element defines the maximum number of minutes for which a cron job can be scheduled. After
this time, the schedule entry for the cron job will be removed from the schedule tables.

Example:

```xml
<schedule_lifetime>2</schedule_lifetime>
```

### `<history_cleanup_every>`

The `<history_cleanup_every>` element determines how often the cron history is cleaned up. It sets the frequency in
minutes for cleaning up the history of executed cron jobs.

Example:

```xml
<history_cleanup_every>10</history_cleanup_every>
```

### `<history_success_lifetime>`

The `<history_success_lifetime>` element specifies the number of minutes after which successful cron job entries are
removed from the history tables.

Example:

```xml
<history_success_lifetime>60</history_success_lifetime>
```

### `<history_failure_lifetime>`

The `<history_failure_lifetime>` element defines the number of minutes after which failed cron job entries are removed
from the history tables.

Example:

```xml
<history_failure_lifetime>600</history_failure_lifetime>
```

### `<use_separate_process>`

The `<use_separate_process>` element determines whether cron jobs assigned to the cron group should be executed in a
separate process. It accepts a boolean value: `0` for false and `1` for true.

Example:

```xml
<use_separate_process>0</use_separate_process>
```

## Conclusion

The `cron_groups.xml` file is a crucial configuration file used in Magento 2 for defining cron groups and their
associated cron jobs. By understanding its structure and the various elements and attributes it provides, you can
effectively manage and schedule cron jobs within your Magento 2 module.

Remember to make any necessary modifications to this file with caution, as incorrect configurations may lead to
unexpected behaviors or issues with your cron jobs.
