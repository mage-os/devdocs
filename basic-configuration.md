---
description: Explore the Mage-OS Basic Configuration guide for setting up system preferences, store settings, payment methods, and shipping options in Magento 2. Perfect for tailoring your eCommerce site to business needs.
keywords: Mage-OS, Magento 2 configuration, basic settings, store setup, payment methods, shipping configuration, eCommerce, system settings, Magento 2 guide, Magento store customization, Magento basic setup
---
# Basic Configuration Documentation

[TOC]

This document provides instructions on how to perform basic configuration in Magento 2. Magento 2 is a powerful
e-commerce platform built on PHP, and understanding how to configure it is essential for creating a successful online
store. In this guide, we will cover the most important configuration settings and provide concrete examples and code
snippets to help you understand and implement them.

## System Configuration

The system configuration in Magento 2 allows you to set up and manage various aspects of your e-commerce store.

To access the system configuration, follow these steps:

1. Log in to the Magento 2 admin panel.
2. Navigate to **Stores** > **Configuration**.

### Example: Changing the Base URL

One of the most crucial system configuration settings is the Base URL. This setting determines the URL that customers
will use to access your store.

To change the Base URL:

1. Go to **Stores** > **Configuration**.
2. In the left-hand menu, click on **General** > **Web**.
3. Expand the **Base URLs (Secure)** or **Base URLs (Unsecure)** section, depending on your requirements.
4. Enter the desired URL in the **Base URL** field.
5. Click on **Save Config**.

## Store Configuration

Store configuration settings in Magento 2 allow you to customize various aspects related to your store's appearance and
functionality.

To access the store configuration, follow these steps:

1. Log in to the Magento 2 admin panel.
2. Navigate to **Stores** > **Configuration**.

### Example: Changing the Store Name

The store name is displayed prominently on your website and should reflect your brand and business.

To change the store name:

1. Go to **Stores** > **Configuration**.
2. In the left-hand menu, click on **General** > **Store Information**.
3. Enter the desired store name in the **Store Name** field.
4. Click on **Save Config**.

## Catalog Configuration

Catalog configuration settings in Magento 2 allow you to manage how your products are displayed, categorized, and
priced.

To access the catalog configuration, follow these steps:

1. Log in to the Magento 2 admin panel.
2. Navigate to **Stores** > **Configuration**.

### Example: Setting Up Product Categories

Product categories help customers navigate your store and find the products they are looking for. To set up product
categories:

1. Go to **Stores** > **Configuration**.
2. In the left-hand menu, click on **Catalog** > **Catalog**.
3. Expand the **Category Top Navigation** section.
4. Enable the **Enable Category Top Navigation Menu** option.
5. Click on **Save Config**.

## Payment Configuration

Payment configuration settings in Magento 2 allow you to set up and manage the payment methods available to your
customers.

To access the payment configuration, follow these steps:

1. Log in to the Magento 2 admin panel.
2. Navigate to **Stores** > **Configuration**.

### Example: Enabling PayPal Express Checkout

PayPal Express Checkout is a popular payment method. To enable PayPal Express Checkout:

1. Go to **Stores** > **Configuration**.
2. In the left-hand menu, click on **Sales** > **Payment Methods**.
3. Expand the **PayPal Express Checkout** section.
4. Set the **Enabled** option to **Yes**.
5. Enter your PayPal API credentials in the appropriate fields.
6. Click on **Save Config**.

## Shipping Configuration

Shipping configuration settings in Magento 2 allow you to manage how shipping is calculated and handled in your store.

To access the shipping configuration, follow these steps:

1. Log in to the Magento 2 admin panel.
2. Navigate to **Stores** > **Configuration**.

### Example: Configuring Flat Rate Shipping

Flat rate shipping charges a fixed rate for shipping regardless of the order's weight or location. To configure flat
rate shipping:

1. Go to **Stores** > **Configuration**.
2. In the left-hand menu, click on **Sales** > **Shipping Methods**.
3. Expand the **Flat Rate** section.
4. Set the **Enabled** option to **Yes**.
5. Configure the **Title**, **Method Name**, **Price**, and other relevant fields.
6. Click on **Save Config**.

## Conclusion

In this documentation, we have covered the basic configuration settings in Magento 2, including system, store, catalog,
payment, and shipping configurations. By following the provided instructions and using the code snippets and examples,
you can easily configure your Magento 2 store to meet your specific requirements. For more advanced configuration
options, refer to the official Magento 2 documentation or consult with a Magento developer.
