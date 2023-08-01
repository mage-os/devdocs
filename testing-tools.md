# Testing Tools Documentation

[TOC]

## Introduction

In this documentation, we will explore various testing tools that can be utilized for testing PHP and Magento 2
applications. Testing is an essential aspect of software development, ensuring the quality and reliability of your code.
These tools facilitate the process by automating test execution, providing detailed reports, and assisting in code
coverage analysis. Let's dive into the world of testing tools!

## PHPUnit

PHPUnit is a widely-used testing framework for PHP applications. It provides a rich set of assertions, test case
management, and test execution capabilities. With PHPUnit, you can write unit tests to validate individual components of
your code, such as classes, methods, and functions.

### Installation

To install PHPUnit, you can utilize Composer, the dependency management tool for PHP. Open a terminal or command prompt
and execute the following command:

```shell
composer require --dev phpunit/phpunit
```

### Example

Let's take a look at a basic PHPUnit test case for a Magento 2 module. Assume we have a module named `My_Module` with a
class `MyClass` containing a `sum` method. We want to test if the method correctly adds two numbers.

```php
class MyClassTest extends \PHPUnit\Framework\TestCase
{
    public function testSum()
    {
        $myClass = new \My\Module\MyClass();
        $result = $myClass->sum(2, 3);
        
        $this->assertEquals(5, $result);
    }
}
```

In this example, we create a test case class `MyClassTest` that extends the `TestCase` class provided by PHPUnit.
The `testSum` method defines our test scenario. We create an instance of `MyClass`, call the `sum` method with
inputs `2` and `3`, and assert that the returned result is `5` using the `assertEquals` assertion.

### Running Tests

To execute PHPUnit tests, navigate to the root directory of your project in a terminal or command prompt and run the
following command:

```shell
./vendor/bin/phpunit
```

PHPUnit will automatically discover and execute all test cases within your project. It will display the test results,
including the number of tests executed, failures, and errors.

## Magento Testing Framework (MTF)

The Magento Testing Framework (MTF) is a powerful tool specifically designed for testing Magento 2 applications. It
offers a comprehensive set of functionalities for integration, functional, and performance testing. MTF integrates with
PHPUnit and provides additional capabilities tailored for Magento 2, such as fixture management and test data
generation.

### Installation

MTF is part of the Magento 2 development environment. To install it, follow the Magento 2 installation instructions
provided by Magento.

### Example

Let's consider an example where we want to test a Magento 2 controller. We have a module named `My_Module` with a
controller `Index` that returns a JSON response. We want to verify if the response contains the expected data structure.

```php
class IndexTest extends \Magento\TestFramework\TestCase\AbstractController
{
    public function testExecute()
    {
        $this->dispatch('my_module/index/index');
        $responseBody = $this->getResponse()->getBody();

        $this->assertJson($responseBody);
        $this->assertArrayHasKey('data', json_decode($responseBody, true));
    }
}
```

In this example, we create a test case class `IndexTest` that extends the `AbstractController` class provided by MTF.
The `testExecute` method dispatches a request to the `my_module/index/index` URL and retrieves the response body. We
assert that the response is in JSON format using `assertJson` and check if the decoded response body contains the `data`
key using `assertArrayHasKey`.

### Running Tests

To execute MTF tests, navigate to the root directory of your Magento 2 project in a terminal or command prompt and run
the following command:

```shell
vendor/bin/phpunit -c dev/tests/integration/phpunit.xml.dist
```

MTF tests are typically stored in the `dev/tests/integration/testsuite` directory of your Magento 2 project. PHPUnit is
used to execute the tests, and the `-c` option specifies the PHPUnit configuration file to use.

## Codeception

Codeception is a versatile testing framework that supports various testing styles, including unit, functional, and
acceptance testing. It provides a simple and intuitive syntax for test case creation and execution. Codeception also
integrates with popular PHP frameworks, including Magento 2, making it an excellent choice for testing Magento
applications.

### Installation

To install Codeception, utilize Composer. Open a terminal or command prompt and execute the following command:

```shell
composer require --dev codeception/codeception
```

### Example

Let's demonstrate a basic Codeception acceptance test for a Magento 2 module. Assume we have a module named `My_Module`
with a page accessible at `/my_module/index/index`. We want to verify if the page title matches the expected value.

```php
class MyModuleCest
{
    public function testHomePage(\AcceptanceTester $I)
    {
        $I->amOnPage('/my_module/index/index');
        $I->seeInTitle('My Module Home');
    }
}
```

In this example, we create a Cest class `MyModuleCest` that defines a test method `testHomePage`. The `$I` object
represents the test actor and provides various assertion and action methods. We use `$I->amOnPage` to navigate to the
desired URL and `$I->seeInTitle` to assert the presence of a specific text in the page title.

### Running Tests

To execute Codeception tests, navigate to the root directory of your project in a terminal or command prompt and run the
following command:

```shell
vendor/bin/codecept run
```

Codeception will automatically discover and execute all test suites within your project. It will display the test
results, including the number of tests executed, failures, and errors.

## Conclusion

Testing tools like PHPUnit, MTF, and Codeception play a crucial role in ensuring the quality and stability of your PHP
and Magento 2 applications. With their capabilities, you can automate the testing process, validate your code, and
identify potential issues. By incorporating these tools into your development workflow, you can confidently release
software that meets the highest standards of quality. Happy testing!
