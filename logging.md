# Logging Documentation

[TOC]

## Introduction

Logging is an essential process in software development that allows developers to collect and record information about
the execution of their code. It helps in troubleshooting, debugging, and monitoring applications. In this documentation,
we will explore the concept of logging, its importance, and how to effectively implement logging in PHP and Magento 2.

## What is Logging?

Logging is the practice of recording information about the execution of software applications. It involves capturing
relevant data and storing it in a structured format for analysis and reference. This information can include error
messages, warnings, debug statements, performance metrics, and more.

Logging provides developers with a detailed record of events that occur during the execution of their code. This record
can be used to identify and diagnose issues, track user behavior, and monitor the health and performance of an
application.

## Why is Logging Important?

Logging plays a crucial role in software development for several reasons:

- **Debugging**: When errors or unexpected behavior occur, logging helps developers understand what went wrong by
  providing valuable information about the context in which the error occurred.
- **Troubleshooting**: Logging allows developers to trace the execution flow and identify potential bottlenecks or areas
  of improvement.
- **Monitoring**: By logging performance metrics, developers can analyze the behavior of their application over time,
  identify areas for optimization, and ensure the application meets its performance goals.
- **Compliance**: Logging can be essential for meeting regulatory requirements, such as tracking user actions or
  maintaining an audit trail.

Proper logging practices ensure that developers have the necessary information to diagnose and resolve issues quickly,
leading to more reliable and maintainable software.

## Logging Levels

Logging levels provide a way to categorize and prioritize different types of log messages based on their significance.
Common logging levels include:

- **Debug**: Detailed information for debugging purposes, typically used during development.
- **Info**: General information about the execution flow or significant events.
- **Warning**: Indications that something unexpected happened, but the application can continue to function.
- **Error**: Errors that prevent the application from functioning correctly.
- **Critical**: Critical errors that require immediate attention and may result in the application's failure.

By assigning appropriate logging levels to log messages, developers can filter and analyze logs based on their severity,
making it easier to focus on critical issues.

## Logging in PHP

PHP provides several logging mechanisms to capture and store log information. One commonly used approach is to utilize
the built-in logging functions provided by the PHP core, such as `error_log()` or `trigger_error()`.

### Example: Basic Logging in PHP

```php
// Log a message with the 'debug' level
error_log("Debug message", 3, "/path/to/logfile.log");

// Log an error message with the 'error' level
trigger_error("Something went wrong", E_USER_ERROR);
```

In the example above, the `error_log()` function is used to log a message with the level set to 'debug'. The log message
is written to the specified log file `/path/to/logfile.log`. Similarly, the `trigger_error()` function is used to log an
error message with the 'error' level.

By adjusting the log levels and destinations, developers can control which messages are logged and where they are
stored.

## Logging in Magento 2

Magento 2, a popular e-commerce platform, provides a robust logging system that allows developers to capture and manage
log messages from various parts of the application.

Magento 2 uses the Monolog library, a powerful logging library, as its logging framework. Developers can take advantage
of Monolog's features, such as logging to different channels, formatting log messages, and filtering log levels.

### Example: Logging in Magento 2

```php
use Psr\Log\LoggerInterface;

class CustomClass
{
    protected $logger;

    public function __construct(LoggerInterface $logger)
    {
        $this->logger = $logger;
    }

    public function doSomething()
    {
        // Log an info message
        $this->logger->info('Something happened');

        try {
            // Business logic
        } catch (\Exception $e) {
            // Log an error message with the exception details
            $this->logger->error('An error occurred', ['exception' => $e]);
        }
    }
}
```

In the example above, we have a custom class that utilizes Magento 2's logging capabilities. The `LoggerInterface` is
injected into the class's constructor, providing access to the logger instance.

Inside the `doSomething()` method, an info message is logged using the `info()` method of the logger. Additionally, an
error message is logged within a try-catch block, including the exception details as additional context information.

By leveraging Magento 2's logging system, developers can easily capture relevant information throughout the application
and analyze it using various tools and techniques.

## Conclusion

Logging is an indispensable part of software development, allowing developers to track and analyze the execution of
their code. By understanding the importance of logging, the different logging levels, and the available logging
mechanisms in PHP and Magento 2, developers can effectively implement logging in their applications. Proper logging
practices contribute to faster issue resolution, improved application performance, and enhanced debugging capabilities.
