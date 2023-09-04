# Integration Testing in Magento 2

- [Integration Testing in Magento 2](#integration-testing-in-magento-2)
- [Overview](#overview)
- [Running Integration Tests in Magento 2](#running-integration-tests-in-magento-2)
- [Setting Up the Integration Test Framework](#setting-up-the-integration-test-framework)
    - [Command Line Interface (CLI)](#command-line-interface)
    - [PhpStorm IDE](#phpstorm-ide)
- [Preparing Integration Test Execution](#preparing-integration-test-execution)
    - [Integration Test Database](#integration-test-database)
    - [Configuring the Framework for Test Environment](#configuring-the-framework-for-test-environment)
    - [Adjusting the PHPUnit Configuration File](#adjusting-the-phpunit-configuration-file)
        - [TESTS_CLEANUP Constant](#tests-cleanup-constant)
- [Executing Third-Party Integration Tests](#executing-third-party-integration-tests)
- [Running Integration Tests in the CLI](#running-integration-tests-in-the-cli)
    - [Running All Integration Tests](#running-all-integration-tests)
    - [Running Only a Custom Test Suite](#running-only-a-custom-test-suite)
    - [Running Tests from a Specific Directory Tree](#running-tests-from-a-specific-directory-tree)
    - [Running a Single Test Class](#running-a-single-test-class)
    - [Running a Single Test within a Test Class](#running-a-single-test-within-a-test-class)
- [Common Mistakes](#common-mistakes)
    - [Could Not Read Files Specified as Arguments](#could-not-read-files-specified-as-arguments)
    - [Could Not Read “dev/tests/integration/phpunit.xml”](#could-not-read-dev-tests-integration-phpunit-xml)
    - [Unable to Connect to MySQL](#unable-to-connect-to-mysql)
- [Running Integration Tests in PhpStorm](#running-integration-tests-in-phpstorm)
    - [Creating an Integration Test Run Configuration](#creating-an-integration-test-run-configuration)
    - [Using the Integration Test Configuration File](#using-the-integration-test-configuration-file)
- [Using Data Providers in Integration Tests](#using-data-providers-in-integration-tests)
    - [Creating a Data Provider](#creating-a-data-provider)
    - [Using a Data Provider](#using-a-data-provider)
    - [Benefits of Using Data Providers](#benefits-of-using-data-providers)
- [Using Fixtures in Integration Tests](#using-fixtures-in-integration-tests)
    - [Creating Fixtures](#creating-fixtures)
    - [Using Fixtures](#using-fixtures)
    - [Fixture Rollback Scripts](#fixture-rollback-scripts)
    - [Benefits of Using Fixtures](#benefits-of-using-fixtures)
- [Understanding DocBlock Annotations in Magento 2 Integration Tests](#understanding-docblock-annotations-in-magento-2-integration-tests)
    - [@magentoDataFixture](#magentodatafixture)
    - [@magentoDbIsolation](#magentodbisolation)
    - [@magentoAppIsolation](#magentoappisolation)
    - [@magentoConfigFixture](#magentoconfigfixture)
    - [@magentoAppArea](#magentoapparea)
    - [@magentoCache](#magentocache)

<a href="#overview"></a>

## Overview

Integration testing is a crucial phase in the software development lifecycle that involves testing individual software
modules as a group. The primary purpose of integration testing is to expose faults in the interaction between integrated
units. It is conducted to evaluate the compliance of a system or component with specified functional requirements.

In the context of software development, integration tests play a pivotal role in ensuring that the different pieces of a
system work together as expected. These tests are typically written to test the interaction between different parts of
the system, such as modules, functions, or services. They can help identify issues with the system's interfaces,
performance, and behavior.

While unit tests focus on verifying the correctness of individual components in isolation, integration tests ensure that
the system works correctly as a whole. They are designed to detect any inconsistencies between the software units that
are integrated together.

Integration tests are particularly important in complex systems where components are developed separately or in
parallel. They help ensure that changes or additions to one part of the system do not break other parts. They also help
verify that the system meets its overall functional and performance requirements.

Now, let's dive into the specifics of running integration tests in Magento 2.

<a href="#running-integration-tests-in-magento-2"></a>

## Running Integration Tests in Magento 2

Integration tests in Magento 2 require a runtime environment, necessitating some preparation before execution. These
tests can be run using the command line interface (CLI) or within an Integrated Development Environment (IDE) like
PhpStorm.

<a href="#setting-up-the-integration-test-framework"></a>

## Setting Up the Integration Test Framework

To execute integration tests, you need to create and configure a test database. Depending on your requirements, you
might also want to adjust the PHPUnit configuration. For more details, refer to the section on Preparing Integration
Test Execution.

<a href="#command-line-interface"></a>

### Command Line Interface (CLI)

The CLI is a suitable option for running tests locally during development or on remote servers during continuous
integration. For more information, refer to the section on Running Integration Tests in the CLI.

<a href="#phpstorm-ide"></a>

### PhpStorm IDE

Running integration tests within an IDE like PhpStorm is convenient during development, especially when writing a new
integration test. However, apart from convenience, there are no additional benefits over running the tests on the
console. For more information, refer to the section on Running Integration Tests in PhpStorm.

<a href="#preparing-integration-test-execution"></a>

## Preparing Integration Test Execution

Before using the Magento integration test framework, you need to prepare the test environment. This involves setting up
a dedicated integration test database, configuring the test framework database, and ensuring the PHPUnit configuration
aligns with the purpose of the integration test execution.

<a href="#integration-test-database"></a>

### Integration Test Database

By default, the test framework installs a fresh Magento test database for every integration test run. It's crucial not
to use the same database as your live Magento instance, as all data, including products, customers, orders, etc., will
be lost.

For safety, it's recommended to use a dedicated database user for running the tests. This user should not have access to
any other databases. Here's an example of SQL commands that create a test database and a dedicated test user account:

```sql
CREATE
DATABASE magento_integration_tests;
GRANT ALL
ON magento_integration_tests.* TO 'magento2_test_user'@'localhost' IDENTIFIED BY 'magento2_test_password';
```

Remember to replace the example database, username, and password with ones that suit your requirements and conventions.

<a href="#configuring-the-framework-for-test-environment"></a>

### Configuring the Framework for Test Environment

The Magento 2 integration test framework provides a configuration file template located
at `dev/tests/integration/etc/install-config-mysql.php.dist`.

Copy this file to `dev/tests/integration/etc/install-config-mysql.php` (without the `.dist` suffix) and add your
test database access credentials. The contents will look similar to the following:

```php
<?php

return [
    'db-host' => 'localhost',
    'db-user' => 'magento2_test_user',
    'db-password' => 'magento2_test_password',
    'db-name' => 'magento_integration_tests',
    'db-prefix' => '',
    'backend-frontname' => 'backend',
    'admin-user' => \Magento\TestFramework\Bootstrap::ADMIN_NAME,
    'admin-password' => \Magento\TestFramework\Bootstrap::ADMIN_PASSWORD,
    'admin-email' => \Magento\TestFramework\Bootstrap::ADMIN_EMAIL,
    'admin-firstname' => \Magento\TestFramework\Bootstrap::ADMIN_FIRSTNAME,
    'admin-lastname' => \Magento\TestFramework\Bootstrap::ADMIN_LASTNAME,
    'amqp-host' => 'localhost',
    'amqp-port' => '5672',
    'amqp-user' => 'guest',
    'amqp-password' => 'guest',
];
```

Leave all the settings that do not start with `db-` and `amqp-` at their default values. You can include additional
setup options available to the `setup:install` command in the test configuration file.

<a href="#adjusting-the-phpunit-configuration-file"></a>

### Adjusting the PHPUnit Configuration File

The default integration test configuration is located in the `dev/tests/integration/phpunit.xml.dist` file. Without
adjustments, this configuration runs all core integration tests, which is useful on a continuous integration server.

When making adjustments to the configuration, copy the default file to `dev/tests/integration/phpunit.xml` (without
the `.dist` suffix) and make your changes there. This ensures your changes won't be overwritten during Magento upgrades.

There are many settings in the file. This guide will only describe three common adjustments. For more information about
the available configuration settings, refer to
the [PHPUnit documentation](https://phpunit.readthedocs.io/en/9.5/configuration.html) and comments in the default file.

<a href="#tests-cleanup-constant"></a>

#### TESTS_CLEANUP Constant

The default value for the `TESTS_CLEANUP` constant is `enabled`. If set to `enabled`, the integration test framework
cleans the test database and reinstalls Magento on every test run. This ensures any new modules are automatically picked
up and any artifacts left behind by previous test runs are removed. It also causes the test framework to flush the test
Magento configuration, the cache, and the code generation before executing any tests.

The downside of setting `TEST_CLEANUP` to `enabled` is that the reinstallation of Magento takes time. The exact time
depends on the host you are using to run the integration tests and the Magento version.

During the development of new integration tests, where only a subset of the tests is executed repeatedly, the overhead
of setting up a fresh execution environment for each run can quickly become a burden. In that case, the `TEST_CLEANUP`
constant can be set to `disabled`. The test execution will start much quicker, but as a consequence, the developer must
manually flush the cache and the database when needed.

The integration test framework creates the temporary test files beneath the
directory `dev/tests/integration/tmp/sandbox-*` (followed by a long hash ID). To force the test framework to regenerate
the cache and the other files, remove the directory:

```bash
rm -r dev/tests/integration/tmp/sandbox-*
```

<a href="#executing-third-party-integration-tests"></a>

## Executing Third-Party Integration Tests

Magento code integration tests reside in the `dev/tests/integration/testsuite` directory. For core tests, it makes sense
that the integration tests do not reside within individual modules, because most integration tests execute code from
many different modules.

Specific integration tests for shop implementation could also be placed within a different subdirectory of
`dev/tests/integration/testsuite`, and then would be executed together with the core tests.

However, third-party extensions are contained within a single directory and might supply custom integration tests too.
These tests usually reside in the `Test/Integration/` subdirectory within the module folder.

These third-party integration tests are not picked up by the default integration test configuration. You can add a test
suite configuration, like the following, to the `<testsuites>` section of the `phpunit.xml` file so they are included
during test execution.

```xml

<testsuite name="Third Party Integration Tests">
    <directory>../../../app/code/*/*/Test/Integration</directory>
    <directory>../../../vendor/*/module-*/Test/Integration</directory>
    <exclude>../../../app/code/Magento</exclude>
    <exclude>../../../vendor/magento</exclude>
</testsuite>
```

Such a test suite configuration can then be executed using the `--testsuite <name>` command option. For example, if you
are in the `dev/tests/integration` directory:

```bash
php ../../../vendor/bin/phpunit --testsuite "Third Party Integration Tests"
```

<a href="#running-integration-tests-in-the-cli"></a>

## Running Integration Tests in the CLI

The most common way to execute integration tests is using the CLI. Ensure you have prepared the integration test
environment before starting.

Integration tests must be executed from the `dev/tests/integration` working directory. The test configuration resides in
that directory and will be picked up by `phpunit` automatically, without the need to specify it as a command line
option.

<a href="#running-all-integration-tests"></a>

### Running All Integration Tests

By default, if no additional arguments are specified, the test configuration executes all integration tests in
the `dev/tests/integration/testsuite` directory.

```bash
cd dev/tests/integration
../../../vendor/bin/phpunit
```

<a href="#running-only-a-custom-test-suite"></a>

### Running Only a Custom Test Suite

PHPUnit offers several ways to only execute a subset of tests. For example, it is common to only execute a single test
suite from the `phpunit.xml` configuration.

```bash
cd dev/tests/integration
../../../vendor/bin/phpunit --testsuite "Memory Usage Tests"
```

<a href="#running-tests-from-a-specific-directory-tree"></a>

### Running Tests from a Specific Directory Tree

To execute only the tests within a specific directory (for example an extension), pass the path to that directory as an
argument to `phpunit`:

```bash
cd dev/tests/integration
../../../vendor/bin/phpunit ../../../app/code/Acme/Example/Test/Integration
```

<a href="#running-a-single-test-class"></a>

### Running a Single Test Class

When developing a new integration test class, it is common to run only that single test many times. Pass the path to the
file containing the test class as an argument to `phpunit`:

```bash
cd dev/tests/integration
../../../vendor/bin/phpunit ../../../app/code/Acme/Example/Test/Integration/ExampleTest.php
```

<a href="#running-a-single-test-within-a-test-class"></a>

### Running a Single Test within a Test Class

You can run only a single test within a test class by specifying the test class together with the `--filter` argument
and the name to select the test that you are currently developing:

```bash
cd dev/tests/integration
../../../vendor/bin/phpunit --filter 'testOnlyThisOneIsExecuted' ../../../app/code/Acme/Example/Test/Integration/ExampleTest.php
```

<a href="#common-mistakes"></a>

## Common Mistakes

<a href="#could-not-read-files-specified-as-arguments"></a>

### Could Not Read Files Specified as Arguments

This error occurs if the integration tests are executed from the wrong directory.

<a href="#could-not-read-dev-tests-integration-phpunit-xml"></a>

### Could Not Read “dev/tests/integration/phpunit.xml”

This error occurs if the integration tests are executed from a different directory than `dev/tests/integration`. To fix
the issue, change to the `dev/tests/integration` directory, adjust any relative paths accordingly, and run the tests
again.

<a href="#unable-to-connect-to-mysql"></a>

### Unable to Connect to MySQL

The PHP interpreter must be able to connect to the test database. By default, this means the tests have to run on the
same host as the MySQL server. This problem most commonly occurs during development with Vagrant or Docker, where the
Magento database is running on a virtual machine. If the tests then are executed using a PHP interpreter on the host
system, the database might not be accessible.

The error usually looks something like this:

```bash
phpunit

Expected log

exception 'PDOException' with message 'SQLSTATE[HY000] [2002] No such file or directory' in /var/www/magento2/vendor/magento/zendframework1/library/Zend/Db/Adapter/Pdo/Abstract.php:129
```

There are many ways this problem can be resolved, but the easiest is to run the tests in the virtual machine as well.

<a href="#running-integration-tests-in-phpstorm"></a>

## Running Integration Tests in PhpStorm

When writing new integration tests or during debugging, it is convenient to execute tests from within the PhpStorm IDE.
Ensure you have prepared the integration test environment before starting.

<a href="#creating-an-integration-test-run-configuration"></a>

### Creating an Integration Test Run Configuration

Setting up a run configuration for integration tests is very similar to creating a run configuration for unit tests. See
Running Unit Tests in PhpStorm for instructions on creating a basic run configuration. Then, configure the integration
test to use the configuration file.

<a href="#using-the-integration-test-configuration-file"></a>

### Using the Integration Test Configuration File

The only difference in the run configuration is that the integration test `phpunit.xml.dist` or `phpunit.xml`
configuration file from the `dev/tests/integration` directory must be selected.

<a href="#using-data-providers-in-integration-tests"></a>

## Using Data Providers in Integration Tests

Data providers are a powerful feature of PHPUnit that allow you to run a test multiple times with different data sets.
They are methods that return an array of arrays, where each array is the set of parameters that will be used for a run
of the test.

<a href="#creating-a-data-provider"></a>

### Creating a Data Provider

A data provider method must be public and either return an array of arrays or an object that implements the `Iterator`
interface and yields an array for each iteration. Each array is a set of parameters for the test method.

Here's an example of a data provider:

```php
public function provider()
{
    return [
        ['value1', 'value2'],
        ['value3', 'value4'],
    ];
}
```

<a href="#using-a-data-provider"></a>

### Using a Data Provider

To use a data provider, add the `@dataProvider` annotation to your test method and specify the name of the data provider
method. The test method will then be run once for each set of parameters returned by the data provider.

```php
/**
 * @dataProvider provider
 */
public function testMethod($param1, $param2)
{
    // Test code here
}
```

In this example, `testMethod` would be run twice: once with `$param1` set to `'value1'` and `$param2` set to `'value2'`,
and once with `$param1` set to `'value3'` and `$param2` set to `'value4'`.

<a href="#benefits-of-using-data-providers"></a>

### Benefits of Using Data Providers

Data providers can help you write more efficient and effective tests. They allow you to easily test a method with a
variety of data, which can help you ensure that your code works correctly in different scenarios. They also make your
tests more readable and maintainable, as you can easily see the data that is being used for each test and add or remove
data sets as needed.

<a href="#using-fixtures-in-integration-tests"></a>

## Using Fixtures in Integration Tests

In the context of testing, a fixture is a fixed state of a set of objects used as a baseline for running tests. The
purpose of a test fixture is to ensure that there is a well-known and fixed environment in which tests are run so that
results are repeatable. Examples of fixtures:

- Preparation of input data and setup/creation of fake or mock objects
- Loading a database with a specific, known set of data
- Copying a specific known set of files creating a test fixture will create a set of objects initialized to certain
  states.

<a href="#creating-fixtures"></a>

### Creating Fixtures

In Magento 2, fixtures are PHP scripts that set required preconditions. Here is an example of a fixture script:

```php
<?php
require 'default_rollback.php';
require __DIR__ . '/../../Customer/_files/customer_rollback.php';
require __DIR__ . '/../../Store/_files/second_website_with_two_stores_rollback.php';
require __DIR__ . '/../../Store/_files/second_website_with_store_group_and_store_rollback.php';
```

This script includes other scripts that set up the necessary preconditions for the test. There are many predefined
fixtures for the most common needs located under `/dev/tests/integration/testsuite/Magento/*/_files`. For example, the
fixture to create an order in your test is located
under `dev/tests/integration/testsuite/Magento/Sales/_files/order.php`.

You can use your own fixtures by adding the path to the fixture script to the `@magentoDataFixture` annotation in your
test method. 

```php
/**
 * @magentoDataFixture ../../../../app/code/Vendor/Module/Test/Integration/_files/my_custom_fixture.php
 */
public function testMethod()
{
    // Test code here
}
```

<a href="#using-fixtures"></a>

### Using Fixtures

To use a fixture in your test, you need to add a special annotation to your test method:

```php
/**
 * @magentoDataFixture Magento/Catalog/_files/categories.php
 */
public function testMethod()
{
    // Test code here
}
```

In this example, before `testMethod` is run, the `categories.php` fixture script will be executed. This script will set
up the necessary preconditions for the test. The `@magentoDataFixture Magento/Catalog/_files/categories.php` annotation
will resolve to `dev/tests/integration/testsuite/Magento/Catalog/_files/categories.php`.

<a href="#fixture-rollback-scripts"></a>
### Fixture Rollback Scripts

Magento 2 also allows you to create rollback scripts for your fixtures. These scripts are used to return the system to
its previous state after the test is run. This is useful for cleaning up any changes that were made during the test.

Rollback scripts are named the same as the fixture script, but with `_rollback` appended to the name. For example, the
rollback script for `categories.php` would be `categories_rollback.php`.

To use a rollback script, you don't need to do anything special in your test method. Magento 2 will automatically run
the appropriate rollback script after each test.

<a href="#benefits-of-using-fixtures"></a>

### Benefits of Using Fixtures

Fixtures allow you to create consistent, repeatable environments for your tests. This can help you ensure that your
tests are reliable and that your code works correctly under different conditions. Fixtures also make your tests easier
to write and understand, as you can clearly see the preconditions for each test.

<a href="#understanding-docblock-annotations-in-magento-2-integration-tests"></a>

## Understanding DocBlock Annotations in Magento 2 Integration Tests

In Magento 2 integration tests, DocBlock annotations are used to provide metadata about the test, such as preconditions,
expectations, and dependencies. Here are some of the most commonly used annotations:

<a href="#magentodatafixture"></a>

### @magentoDataFixture

This annotation is used to specify a fixture script that sets up the necessary preconditions for the test. The script is
run before the test is executed.

```php
/**
 * @magentoDataFixture Magento/Catalog/_files/categories.php
 */
public function testMethod()
{
    // Test code here
}
```

<a href="#magentodbisolation"></a>

### @magentoDbIsolation

This annotation is used to enable or disable database isolation for the test. If database isolation is enabled, any
changes made to the database in the test will be rolled back after the test is run. This helps to ensure test isolation.

```php
/**
 * @magentoDbIsolation enabled
 */
public function testMethod()
{
    // Test code here
}
```

<a href="#magentoappisolation"></a>

### @magentoAppIsolation

This annotation is used to enable or disable application isolation for the test. If application isolation is enabled,
the Magento application is reinitialized after the test is run. This helps to ensure that the state of the application
does not affect other tests.

```php
/**
 * @magentoAppIsolation enabled
 */
public function testMethod()
{
    // Test code here
}
```

<a href="#magentoconfigfixture"></a>

### @magentoConfigFixture

This annotation is used to set a configuration value for the test. The configuration value is set before the test is run
and is restored to its original value after the test is run.

```php
/**
 * @magentoConfigFixture current_store web/unsecure/base_url http://example.com/
 */
public function testMethod()
{
    // Test code here
}
```

<a href="#magentoapparea"></a>

### @magentoAppArea

This annotation is used to set the application area for the test, such as 'frontend', 'adminhtml', 'global', etc. The
application area affects the behavior of the Magento application.

```php
/**
 * @magentoAppArea frontend
 */
public function testMethod()
{
    // Test code here
}
```

<a href="#magentocache"></a>

### @magentoCache

This annotation is used to enable or disable cache types for the test. The cache types are set before the test is run
and are restored to their original state after the test is run.

```php
/**
 * @magentoCache full_page enabled
 */
public function testMethod()
{
    // Test code here
}
```

These annotations provide a powerful way to control the environment in which your tests are run, helping to ensure that
your tests are reliable, repeatable, and isolated from each other.