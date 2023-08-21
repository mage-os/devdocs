# Service Contracts Documentation

[TOC]

Welcome to the Service Contracts documentation! In this guide, we will explore the concept of service contracts in the
context of PHP and Magento 2. Service contracts provide a standardized way to define and interact with modules and their
APIs. By adhering to service contracts, developers can ensure interoperability and maintainability of their codebase.

## Introduction to Service Contracts

In Magento 2, service contracts are interfaces that define a set of methods that can be used to interact with a specific
module or component. By defining a service contract, you establish a clear and consistent API for your module, allowing
other modules to interact with it in a standardized way.

Service contracts provide several benefits, such as:

* **Interoperability**: By adhering to service contracts, your module can seamlessly integrate with other modules that
  depend on your API. This reduces coupling and promotes modularity in the Magento ecosystem.

* **Maintainability**: Service contracts act as a contract between your module and its consumers. This means that you
  can make changes to the underlying implementation of your module without breaking other modules that depend on it, as
  long as you don't change the service contract itself.

* **Testability**: Service contracts provide a clear interface that can be easily mocked and tested. This allows you to
  write unit tests for your module and ensure its functionality in isolation.

## Defining Service Contracts

To define a service contract, you need to create an interface in your module. This interface will contain the methods
that define the API for your module. Let's take a look at an example:

```php
<?php
namespace Vendor\Module\Api;

interface MyServiceInterface
{
    /**
     * Get the greeting message.
     *
     * @param string $name
     * @return string
     */
    public function getGreeting($name);
}
```

In this example, we define a service contract called `MyServiceInterface` in the `Vendor\Module\Api` namespace. It has a
single method called `getGreeting` that takes a `$name` parameter and returns a greeting message.

Remember to add appropriate PHPDoc annotations to document the parameters and return types of your methods. This helps
other developers understand how to use your service contract correctly.

## Implementing Service Contracts

Once you have defined a service contract, you need to implement it in your module. To do this, create a class that
implements the interface and provides the actual implementation of the methods. Here's an example:

```php
<?php
namespace Vendor\Module\Model;

use Vendor\Module\Api\MyServiceInterface;

class MyService implements MyServiceInterface
{
    /**
     * Get the greeting message.
     *
     * @param string $name
     * @return string
     */
    public function getGreeting($name)
    {
        return "Hello, " . $name . "!";
    }
}
```

In this example, we have a class `MyService` that implements the `MyServiceInterface`. It provides the implementation
for the `getGreeting` method, which simply concatenates the name with a greeting message.

Remember to use the same namespace as your service contract when implementing it. This ensures that Magento can
recognize the implementation and use it in the appropriate context.

## Working with Service Contracts

To use a service contract in your module or any other module that depends on it, you need to rely on dependency
injection. This means that you inject the service contract interface into your class constructor or any other method
that requires it.

Here's an example of how to use the `MyServiceInterface` in a Magento 2 class:

```php
<?php
namespace Vendor\Module\Model;

use Vendor\Module\Api\MyServiceInterface;

class MyOtherClass
{
    /**
     * @var MyServiceInterface
     */
    private $myService;

    /**
     * Constructor.
     *
     * @param MyServiceInterface $myService
     */
    public function __construct(MyServiceInterface $myService)
    {
        $this->myService = $myService;
    }

    /**
     * Example method that uses the service contract.
     */
    public function doSomething()
    {
        $greeting = $this->myService->getGreeting("John");
        // Do something with the greeting...
    }
}
```

In this example, we have a class `MyOtherClass` that has a dependency on the `MyServiceInterface`. We inject the service
contract into the class constructor and store it in a private property. Then, we can use the methods defined in the
service contract within the class methods.

By using dependency injection, we ensure that the implementation of the service contract can be easily substituted or
mocked during testing. It also enforces the principle of loose coupling between modules.

## Best Practices

Here are some best practices to keep in mind when working with service contracts:

1. **Keep service contracts focused**: Service contracts should be focused on a specific domain or functionality. Avoid
   creating monolithic service contracts that encompass too many responsibilities.

2. **Be consistent with naming**: Follow Magento's naming conventions when defining service contracts. This helps
   maintain a standardized API across modules.

3. **Document your service contracts**: Use PHPDoc annotations to document the parameters and return types of your
   service contract methods. This makes it easier for developers to understand how to use your module.

4. **Avoid breaking changes**: Once you have defined a service contract, avoid making breaking changes to it. If you
   need to make changes, consider creating a new version of the service contract and mark the old one as deprecated.

## Conclusion

In this documentation, we have explored the concept of service contracts in PHP and Magento 2. Service contracts provide
a standardized way to define and interact with modules, promoting interoperability, maintainability, and testability.

By defining and implementing service contracts, you can create modular and extensible code that can be easily integrated
with other modules in the Magento ecosystem.

Remember to follow best practices, document your service contracts, and leverage dependency injection to ensure loose
coupling and easy testing of your modules.

Happy coding with service contracts in Magento 2!
