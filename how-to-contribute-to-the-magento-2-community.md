# Contributing to the Magento 2 Community

[TOC]

## Introduction

Thank you for your interest in contributing to the vibrant Magento 2 community! Your contributions can help improve the
platform, fix bugs, develop new features, and enhance the overall user experience. This guide will walk you through the
process of contributing to the Magento 2 community, covering everything from setting up your local development
environment to submitting your contributions for review.

## Prerequisites

Before you start contributing to the Magento 2 community, ensure that you have the following prerequisites in place:

1. **Magento 2 instance**: Set up a local development environment with a Magento 2 instance, preferably the latest
   stable version.
2. **Git**: Install Git on your machine to help manage your code changes.
3. **GitHub Account**: Create an account on GitHub if you don't already have one. This will enable you to contribute to
   the Magento 2 repository.

## Clone the Magento 2 Repository

To contribute to the Magento 2 community, you will need to clone the official Magento 2 repository onto your local
machine. Follow these steps to get started:

1. Open your command line interface and navigate to the directory where you want to clone the Magento 2 repository.
2. Run the following command to clone the repository:

```shell
git clone https://github.com/magento/magento2.git
```

3. Once the cloning process completes, navigate into the `magento2` directory using the following command:

```shell
cd magento2
```

## Creating a Branch

Before you start making changes to the Magento 2 codebase, it's important to create a new branch for your contributions.
This ensures that your changes are isolated and can be easily managed. Follow these steps to create a new branch:

1. Ensure that you are in the `magento2` directory.
2. Run the following command to create a new branch:

```shell
git checkout -b my-branch-name
```

Replace `my-branch-name` with a descriptive name for your branch. For example, if you are fixing a bug related to
customer registration, you could use `fix-customer-registration-bug`.

## Making Code Changes

Once you have created a new branch, you can start making code changes to address the issues you want to contribute. Here
are a few examples:

### Example 1: Fixing a bug

If you want to fix a bug, follow these steps:

1. Identify the bug you want to fix.
2. Navigate to the relevant file(s) in the Magento 2 codebase.
3. Make the necessary changes to address the bug.
4. Test your changes to ensure they fix the bug and do not introduce any regressions.

### Example 2: Developing a new feature

If you want to develop a new feature, follow these steps:

1. Identify the feature you want to develop.
2. Plan your implementation and consider the impact on other parts of the codebase.
3. Create new files or modify existing ones to implement the feature.
4. Test your implementation to ensure it works as expected and does not break any existing functionality.

## Running Tests

Before submitting your code changes for review, it is essential to run the tests provided by Magento 2 to ensure that
your changes do not introduce any regressions. Follow these steps to run the tests:

1. Ensure that you are in the `magento2` directory.
2. Run the following command to install the necessary testing dependencies:

```shell
composer install
```

3. Once the installation completes, run the tests using the following command:

```shell
vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist
```

Make sure all tests pass successfully before proceeding.

## Submitting Your Contributions for Review

Once you have made your code changes and ensured that all tests pass, it's time to submit your contributions for review.
Follow these steps to create a pull request (PR) on GitHub:

1. Push your branch to the remote repository using the following command:

```shell
git push origin my-branch-name
```

2. Visit the official Magento 2 repository on
   GitHub: [https://github.com/magento/magento2](https://github.com/magento/magento2).
3. Click on the "Pull requests" tab.
4. Click on the "New pull request" button.
5. Select your branch from the dropdown menu.
6. Add a descriptive title and provide a clear description of your changes.
7. Click on the "Create pull request" button to submit your contributions for review.

## Conclusion

Contributing to the Magento 2 community is an excellent way to improve the platform and collaborate with other
developers. By following the steps outlined in this guide, you can start making a positive impact on the Magento 2
ecosystem. Remember to always adhere to best practices, thoroughly test your changes, and actively engage with the
community for feedback and guidance. Happy contributing!
