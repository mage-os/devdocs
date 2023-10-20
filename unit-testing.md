# Unit Testing in Magento 2

[TOC]

## Overview

Unit testing is a critical part of software development. It involves testing individual units of code (such as functions
or methods) to ensure they perform as expected. In Magento 2, PHPUnit is the testing framework used for writing and
executing unit tests.

Magento 2 has a solid structure for unit tests that separates them from other types of tests (like integration,
functional, and performance tests). In a typical Magento 2 module, the unit tests are located in the `Test/Unit`
directory of the module.

## Setup and Configuration

Before you begin, ensure you have PHPUnit installed. Magento 2 recommends using the latest stable PHPUnit version
supported by your PHP installation.

You can install PHPUnit globally or as a part of your project via Composer. The following command installs PHPUnit
globally:

```bash
composer global require phpunit/phpunit
```

After installing PHPUnit, validate the installation by checking the version:

```bash
phpunit --version
```

## Creating a Unit Test

In this section, we'll create a simple unit test for a hypothetical SampleModule in Magento 2.

1. Navigate to your module's directory and create a new Test/Unit directory if it doesn't exist.

```bash
mkdir -p app/code/Vendor/SampleModule/Test/Unit
```

2. Inside the `Test/Unit` directory, create a new test class. In this case, we'll create `SampleTest.php`:

```php
<?php
declare(strict_types=1);

namespace Vendor\SampleModule\Test\Unit;

class SampleTest extends \PHPUnit\Framework\TestCase
{
    public function testSampleMethod(): void
    {
        $this->assertEquals(10, 5 + 5);
    }
}
```

In this example, `testSampleMethod` is a simple test case that asserts whether `5 + 5` equals `10`.

## Running Unit Tests

To run the unit test, use the phpunit command from the root directory of your Magento 2 installation:

```bash
./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/Vendor/SampleModule/Test/Unit
```

This command tells PHPUnit to use the configuration specified in phpunit.xml.dist and run the tests located
in `app/code/Vendor/SampleModule/Test/Unit`.

To run an entire suite (i.e., all tests in a directory), specify the directory path:

```bash
./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/Vendor/SampleModule/Test/Unit
```

The output should look something like this:

```bash
PHPUnit X.X.X by Sebastian Bergmann and contributors.

.                                       1 / 1 (100%)

Time: X ms, Memory: X MB

OK (1 test, 1 assertion)
```

## Run Unit Tests within PHPStorm

To run tests within PHPStorm, follow these steps:

Open the `Settings/Preferences` dialog (`Ctrl+Alt+S`), go to `Languages & Frameworks | PHP | Test Frameworks`.
Click `+`, and choose `PHPUnit Local`.
Configure the PHPUnit library and settings.
After the configuration, go to your test, right-click on it and select Run `test-name`.

## Write Testable Code

Writing testable code involves designing your code in a way that makes it easier to isolate and test individual units.
Some tips for writing testable code include:

**Single Responsibility**: Each method/class should have a single responsibility. It should do one thing and do it well.
**Avoid Static Methods**: Static methods can't be mocked or stubbed, making them difficult to test.
**Dependency Injection**: Using dependency injection helps make your code more flexible and easier to test.

## Best Practices

**Use Descriptive Test Method Names**: The method name should describe what the test does. For example,
`testUserIsCreatedWithValidInput` is descriptive and you can understand what the test does by looking at its name.
**One Assertion Per Test Method**: Ideally, each test should only have one assertion. This makes the tests more readable
and
errors easier to pinpoint.
**Don't Test Everything**: It's important to note that not all code needs to be tested. If it's already being tested
elsewhere or it's part of the framework's functionality, there's usually no need to test it again.


## Mocking

Mocking is a process used in unit testing when the unit of code has external dependencies. A mock object is a dummy
implementation that simulates the behavior of a real object.

```php
<?php
namespace Vendor\SampleModule\Test\Unit;

use PHPUnit\Framework\TestCase;
use PHPUnit\Framework\MockObject\MockObject;
use Vendor\SampleModule\Model\Sample;

class SampleTest extends TestCase
{
    /**
    * @var MockObject
    */
    private $sampleMock;

    protected function setUp(): void
    {
        $this->sampleMock = $this->getMockBuilder(Sample::class)
            ->disableOriginalConstructor()
            ->getMock();
    }

    public function testSampleMethod()
    {
        $this->sampleMock->method('getNumber')
            ->willReturn(5);

        $this->assertEquals(10, $this->sampleMock->getNumber() + 5);
    }
}
```

In this example, `Sample::class` is a dependency of the unit being tested. We create a mock for this dependency and
define
its behavior to return `5` when getNumber is called.

## DocBlock Annotations

DocBlocks or PHPDoc comments are used to provide metadata for your codebase. These comments can be parsed by tools to
generate human-readable documentation.

PHPUnit uses these annotations to control the behavior of your tests. Here are some commonly used annotations:

- `@test`: This annotation can be used to mark a method as a test method.
- `@dataProvider`: This annotation can be used to specify a method that returns data for a test.
- `@depends`: This annotation can be used to specify that a test depends on another test.
- `@group`: This annotation allows you to group tests together so you can run a set of tests separately from others.

Example:

```php
/**
 * @test
 * @dataProvider additionProvider
 */
public function testAdd($a, $b, $expected)
{
    $this->assertEquals($expected, $a + $b);
}

public function additionProvider()
{
    return [
        [1, 2, 3],
        [0, 0, 0],
        [-1, -1, -2],
    ];
}
```

In this example, `@test` marks `testAdd` as a test method, and `@dataProvider` specifies `additionProvider` as the
method
providing data for the `testAdd` test.

This concludes our in-depth guide on unit testing in Magento 2. Remember that good tests can help you catch bugs early,
make your codebase more maintainable, and save you, your team, and your users a lot of trouble down the line. Happy
testing!


## Code Coverage

Code coverage is a measure that describes the degree to which the source code of a program is executed when a particular
test suite runs. To generate a code coverage report, PHPUnit needs `Xdebug` or `pcov` installed.

You can enable code coverage in the PHPUnit configuration file (phpunit.xml) or run the command:

```bash
./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist --coverage-html coverage app/code/Vendor/SampleModule/Test/Unit
```

This command will generate an HTML report in the `coverage` directory.

## Run Unit Tests in CI

### GitHub Actions

In your `.github/workflows` directory, create a new file called `run-tests.yml` and populate it:

```yaml
name: Run PHPUnit Tests

on: [ push, pull_request ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Validate composer.json and composer.lock
        run: composer validate

      - name: Install Dependencies
        run: composer install --prefer-dist --no-progress --no-suggest

      - name: Run PHPUnit
        run: ./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/Vendor/SampleModule/Test/Unit
```

### GitLab Pipelines

In your .gitlab-ci.yml, add:

```yaml
stages:
  - test

phpunit:
  stage: test
  image: php:latest
  script:
    - composer install
    - ./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/Vendor/SampleModule/Test/Unit
```

## Summary

Unit testing is a vital part of the Magento 2 development process. It helps ensure that your code functions as expected,
which can help reduce bugs and issues in the future. By using PHPUnit, Magento 2 developers can write and run unit tests
to validate their code throughout the development process.
