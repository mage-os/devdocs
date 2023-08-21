# Best Practices for Extension Development

[TOC]

This documentation provides a comprehensive guide on best practices for developing extensions in Magento 2. Following
these guidelines will ensure that your extensions are efficient, secure, and compatible with future versions of Magento.

## Directory Structure <a name="directory-structure"></a>

Organizing your extension's files properly is crucial for maintainability. Follow the recommended directory structure
provided by Magento to ensure consistency across projects.

Here's a typical directory structure for a Magento 2 extension:

```
├── app
│   └── code
│       └── VendorName
│           └── ModuleName
│               ├── Block
│               ├── Controller
│               ├── etc
│               ├── Helper
│               ├── Model
│               ├── Observer
│               ├── Plugin
│               ├── Setup
│               ├── Ui
│               └── view
└── ...
```

## Extension Naming <a name="extension-naming"></a>

Choose a unique, descriptive name for your extension to avoid conflicts with other extensions. Magento recommends using
the following format for naming your extension: `VendorName_ModuleName`.

For example, if your extension is related to a payment gateway named "FastPay" and your company name is "Acme", you
could name your extension `Acme_FastPay`.

## Module Registration <a name="module-registration"></a>

To register your extension with Magento, create a `registration.php` file in the root directory of your extension. This
file should contain a registration callback function that returns an array with the module's name and version.

Here's an example of a `registration.php` file:

```php
<?php

\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Acme_FastPay',
    __DIR__
);
```

## Dependency Injection <a name="dependency-injection"></a>

Magento 2 heavily utilizes dependency injection to manage object dependencies. Follow the dependency inversion principle
and inject dependencies through constructors or setter methods.

Avoid instantiating objects directly using the `new` keyword within your extension. Instead, rely on Magento's
dependency injection framework to provide necessary dependencies.

Here's an example of how to inject a dependency in a constructor:

```php
<?php

namespace Acme\FastPay\Model;

use Acme\FastPay\Api\GatewayInterface;

class Payment
{
    private $gateway;

    public function __construct(
        GatewayInterface $gateway
    ) {
        $this->gateway = $gateway;
    }
}
```

## Event Observers <a name="event-observers"></a>

Magento 2 provides a robust event system that allows extensions to observe and modify the behavior of the core system.
Leverage event observers to extend or customize Magento functionality.

To create an event observer, you need to define the event you want to observe in your extension's `events.xml` file, and
then create a corresponding observer class.

Here's an example of an `events.xml` file:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="sales_order_place_after">
        <observer name="acme_fastpay_order_place_after" instance="Acme\FastPay\Observer\OrderPlaceAfter"/>
    </event>
</config>
```

And here's an example of an observer class:

```php
<?php

namespace Acme\FastPay\Observer;

use Magento\Framework\Event\ObserverInterface;

class OrderPlaceAfter implements ObserverInterface
{
    public function execute(\Magento\Framework\Event\Observer $observer)
    {
        // Handle the event
    }
}
```

## Configuration <a name="configuration"></a>

Provide a user-friendly configuration interface for your extension using the `system.xml` file. This file defines the
configuration fields and sections that appear in the admin panel.

Here's an example of a `system.xml` file:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Config:etc/system_file.xsd">
    <system>
        <tab id="acme" translate="label" sortOrder="10">
            <label>Acme Extensions</label>
        </tab>
        <section id="fastpay" translate="label" type="text" sortOrder="100" showInDefault="1" showInWebsite="1"
                 showInStore="1">
            <label>FastPay Payment Gateway</label>
            <tab>acme</tab>
            <resource>Acme_FastPay::config</resource>
            <group id="general" translate="label" sortOrder="10" type="text" showInDefault="1" showInWebsite="1"
                   showInStore="1">
                <label>General Settings</label>
                <field id="enabled" translate="label comment" type="select" sortOrder="10" showInDefault="1"
                       showInWebsite="1" showInStore="1">
                    <label>Enable FastPay</label>
                    <source_model>Magento\Config\Model\Config\Source\Yesno</source_model>
                </field>
                <!-- Add more fields here as needed -->
            </group>
        </section>
    </system>
</config>
```

## Database Schema and Setup <a name="database-schema-and-setup"></a>

If your extension requires additional database tables or changes to existing tables, follow Magento's recommended
approach for managing database schema and setup.

Create a `db_schema.xml` file to define your extension's database schema. Within this file, you can define tables,
columns, indexes, and other database elements.

Here's an example of a `db_schema.xml` file:

```xml
<?xml version="1.0"?>
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="acme_fastpay_transactions" resource="default" engine="innodb" comment="FastPay Transactions">
        <column xsi:type="int" name="id" padding="10" unsigned="true" nullable="false" comment="Transaction ID"
                identity="true"/>
        <column xsi:type="varchar" name="order_id" nullable="false" length="32" comment="Order ID"/>
        <column xsi:type="decimal" name="amount" nullable="false" scale="2" precision="12"
                comment="Transaction Amount"/>
        <constraint xsi:type="primary" referenceId="PRIMARY">
            <column name="id"/>
        </constraint>
    </table>
</schema>
```

To handle database setup and versioning, create an `InstallSchema.php` file in your extension's `Setup` directory. This
file should contain the necessary logic to create or update your extension's database schema.

Here's an example of an `InstallSchema.php` file:

```php
<?php

namespace Acme\FastPay\Setup;

use Magento\Framework\Setup\InstallSchemaInterface;
use Magento\Framework\Setup\ModuleContextInterface;
use Magento\Framework\Setup\SchemaSetupInterface;

class InstallSchema implements InstallSchemaInterface
{
    public function install(SchemaSetupInterface $setup, ModuleContextInterface $context)
    {
        $installer = $setup->startSetup();

        // Add database schema setup logic here

        $installer->endSetup();
    }
}
```

## Code Quality <a name="code-quality"></a>

Writing clean and well-documented code is essential for maintainability and collaboration. Follow these best practices
to ensure high code quality:

- Follow the [PSR-12 coding style](https://www.php-fig.org/psr/psr-12/) for PHP code.
- Use meaningful variable and function names to improve readability.
- Add inline comments to explain complex or important sections of code.
- Write PHPDoc comments for classes, methods, and properties to provide clear documentation.

## Unit Testing <a name="unit-testing"></a>

Writing unit tests for your extension is crucial to ensure its stability and reliability. Magento provides a robust
testing framework based on PHPUnit.

Create test classes for your extension using the `Test` directory structure. Test classes should be namespaced under the
extension's namespace with the `Test\Unit` suffix.

Here's an example of a test class for a payment gateway extension:

```php
<?php

namespace Acme\FastPay\Test\Unit\Model;

use Acme\FastPay\Model\Payment;
use Magento\Framework\TestFramework\Unit\Helper\ObjectManager;
use PHPUnit\Framework\TestCase;

class PaymentTest extends TestCase
{
    private $objectManager;
    private $payment;

    protected function setUp(): void
    {
        $this->objectManager = new ObjectManager($this);

        $this->payment = $this->objectManager->getObject(
            Payment::class,
            [
                // Inject dependencies here
            ]
        );
    }

    public function testExample()
    {
        // Write your unit tests here
    }
}
```

## Security Considerations <a name="security-considerations"></a>

Ensure the security of your extension by following these best practices:

- Validate and sanitize all user inputs to prevent security vulnerabilities such as SQL injection and cross-site
  scripting.
- Use Magento's built-in security features, such as CSRF protection and form key validation, when handling sensitive
  operations or user data.
- Regularly update your extension to address any security vulnerabilities discovered in dependencies or Magento itself.
- Stay informed about Magento's security practices and guidelines by regularly checking their official documentation and
  security advisories.

## Compatibility <a name="compatibility"></a>

Maintaining compatibility with different versions of Magento is crucial for the longevity and adoption of your
extension. Follow these guidelines to ensure compatibility:

- Keep up-to-date with Magento's latest releases and features to leverage new functionality.
- Avoid using deprecated Magento features or methods.
- Test your extension across different versions of Magento to identify and resolve compatibility issues.
- Clearly communicate the supported Magento versions in your extension's documentation and release notes.

By adhering to these best practices, you can develop high-quality Magento 2 extensions that are secure, efficient, and
compatible across different versions of Magento.
