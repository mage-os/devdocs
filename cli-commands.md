# CLI Commands Documentation

[TOC]

## Introduction

This document provides a comprehensive guide to the Command Line Interface (CLI) commands available in Magento 2. CLI
commands are powerful tools that allow developers and administrators to interact with Magento 2 from the command line.
By executing these commands, you can perform various tasks such as installing or updating modules, flushing caches,
compiling code, and more.

## Prerequisites

Before using the CLI commands, ensure that you have the following prerequisites:

1. A working installation of Magento 2.
2. A command line interface, such as the Terminal or Command Prompt.
3. Familiarity with PHP and Magento 2 concepts.

## Accessing CLI Commands

To access the CLI commands, open a command line interface and navigate to the root directory of your Magento 2
installation. Once you are in the correct directory, you can execute any available CLI command.

## Syntax

The basic syntax for executing a CLI command in Magento 2 is as follows:

```bash
php bin/magento [command_name] [options] [arguments]
```

- `php` refers to the PHP executable.
- `bin/magento` is the entry point for all Magento CLI commands.
- `[command_name]` is the name of the specific command you want to execute.
- `[options]` are additional flags or parameters that modify the behavior of the command.
- `[arguments]` are specific values or variables required by the command.

Note that square brackets indicate optional elements.

## Common CLI Commands

This section provides an overview of some commonly used CLI commands in Magento 2.

### `setup:upgrade`

The `setup:upgrade` command is used to upgrade the Magento 2 instance after installing or updating modules. It applies
database schema and data changes, ensuring that the system is up to date.

Example usage:

```bash
php bin/magento setup:upgrade
```

### `cache:disable`

The `cache:disable` command is used to disable specific cache types within your Magento installation.

Example usage:

```bash
php bin/magento cache:disable full_page
```

### `cache:enable`

The `cache:enable` command in Magento 2 allows you to activate specific cache types to enhance your store's performance by reducing data retrieval times and optimizing resource usage.

Example usage:

```bash
php bin/magento cache:enable full_page
```

### `cache:flush`

The `cache:flush` command flushes all caches in the Magento 2 system. This is useful after making changes that need to
be reflected immediately, such as modifying configuration files or updating module code.

Example usage:

```bash
php bin/magento cache:flush
```

### `cache:status`

The `cache:status` is used to check the current status of cache types in your Magento installation.

Example usage:

```bash
php bin/magento cache:status
```

### `module:enable` and `module:disable`

The `module:enable` and `module:disable` commands allow you to enable or disable specific modules in Magento 2. Enabling
a module activates its functionality, while disabling it renders the module inactive.

Example usage:

```bash
php bin/magento module:enable My_Module
php bin/magento module:disable My_Module
```

### `setup:di:compile`

The `setup:di:compile` command compiles the dependency injection configuration for Magento 2. This step is necessary
after modifying the codebase or adding new modules to ensure that all dependencies are correctly resolved.

Example usage:

```bash
php bin/magento setup:di:compile
```

### `cache:clean`

The `cache:clean` command cleans the Magento 2 cache by removing all cached files. This is useful when troubleshooting
caching issues or when you want to start with a clean cache.

Example usage:

```bash
php bin/magento cache:clean
```

### `deploy:mode:set`

The `deploy:mode:set` command is used to set the operational mode of a Magento store. 

Example usage:

```bash
php bin/magento deploy:mode:set
```

### `deploy:mode:show`

The `deploy:mode:show` quickly displays the current operational mode (default, developer, or production) of your store, assisting in ensuring the optimal mode is active during development and production.

Example usage:

```bash
php bin/magento deploy:mode:show
```

### `store:list`

The `store:list` command provides a list of all the stores within your Magento installation. This includes information about each store's code, website, group, and root category.

Example usage:

```bash
php bin/magento store:list
```

### `store:website:list`

The `store:website:list` command display a list of all websites present in your Magento installation. This command provides essential information about each website, including its code, name, and base URL.

Example usage:

```bash
php bin/magento store:website:list
```

### `maintenance:disable`

The `maintenance:disable` command in Magento 2 is used to disable maintenance mode for your Magento store.

Example usage:

```bash
php bin/magento maintenance:disable
```

### `maintenance:enable`

The `maintenance:enable` command iis designed to activate maintenance mode for your Magento store.

Example usage:

```bash
php bin/magento maintenance:enable
```

### `maintenance:status`

The `maintenance:status` command in Magento 2 is used to display the current status of maintenance mode for your Magento store.

Example usage:

```bash
php bin/magento maintenance:status
```

### `queue:consumers:list`

The `queue:consumers:list` is used to display a list of all message queue consumers in your Magento installation.

Example usage:

```bash
php bin/magento queue:consumers:list
```

### `queue:consumers:restart`

The `queue:consumers:restart` is used to initiate the restart of all message queue consumers. Magento will stop all currently running message queue consumers and then restart them. 

Example usage:

```bash
php bin/magento queue:consumers:restart
```

### `queue:consumers:start`

The `queue:consumers:start` is used to manually start the processing of messages by message queue consumers.

Example usage:

```bash
php bin/magento queue:consumers:start
```

### `indexer:info`

The `indexer:info` is a command that provides information about the indexers in your Magento 2 installation.

Example usage:

```bash
php bin/magento indexer:info
```

### `indexer:reindex`

The `indexer:reindex` command is used to manually trigger the reindexing process for all indexers in your Magento 2 installation. 

Example usage:

```bash
php bin/magento indexer:reindex
```

### `indexer:reset`

The `indexer:reset` is used to reset (invalidate) one or more specific indexers or all indexers. 

Example usage to reset specific index:

```bash
php bin/magento indexer:reset <indexer_code>
```
And to reset all indexers:
```bash
php indexer:reset
```

### `indexer:status`

The `indexer:status` show the status of all indexers in Magento 2.

Example usage:

```bash
php bin/magento indexer:status
```

### `info:adminuri`

The `info:adminuri` is used to display the URL for accessing the Magento Admin Panel

Example usage:

```bash
php bin/magento info:adminuri
```

### `info:backups:list`

The `info:backups:list` command is used to display a list of available backups for your Magento installation.

Example usage:

```bash
php bin/magento info:backups:list
```

### `info:currency:list`

The `info:currency:list` command is used to display a list of available currencies in your Magento installation.

Example usage:

```bash
php bin/magento info:currency:list
```

### `varnish:vcl:generate`

The `varnish:vcl:generate` is used to generate a Varnish Configuration Language (VCL) file and echos it to the console.

Example usage:

```bash
php bin/magento varnish:vcl:generate
```

### `cron:run`

The `cron:run` is used to manually trigger the execution of scheduled cron jobs in your Magento installation.

Example usage:

```bash
php bin/magento cron:run
```

### `config:set`

The `config:set` is used to set or update configuration settings in your Magento installation.

Example usage:

```bash
php bin/magento config:set <path> <value> [--scope="store|website"]
```

In this command:

`<path>` represents the unique identifier or path of the configuration setting you want to modify.

`<value>` is the new value you want to set for the configuration setting.

`--scope` is an optional parameter that allows you to specify whether the configuration change should apply at the store or website level. You can choose "store" or "website."

For example, to set a new value for a specific configuration setting, you would use a command like this:

```bash
php bin/magento config:set mymodule/general/enable_feature 1 --scope="store"
```

## Conclusion

CLI commands in Magento 2 provide a powerful way to interact with the system from the command line. This documentation
has covered some commonly used commands, but Magento 2 offers a wide range of commands for various tasks. By
familiarizing yourself with these commands, you can enhance your development and administration workflow in Magento 2.
