# Magento 2 Directory Structure Documentation

# Table of Contents

1. [Introduction](#introduction)
2. [Overview](#overview)
3. [Key Directories](#key-directories)
    1. [`app/` Directory](#app-directory)
    2. [`bin/` Directory](#bin-directory)
    3. [`dev/` Directory](#dev-directory)
    4. [`generated/` Directory](#generated-directory)
    5. [`lib/` Directory](#lib-directory)
    6. [`pub/` Directory](#pub-directory)
    7. [`pub/media/` Directory](#pubmedia-directory)
    8. [`setup/` Directory](#setup-directory)
    9. [`var/` Directory](#var-directory)
    10. [`vendor/` Directory](#vendor-directory)
4. [`.htaccess` File](#htaccess-file)
6. [Conclusion](#conclusion)

*Please note that each entry is a hyperlink that should direct you to the corresponding section of the document.

<a href="#introduction"></a>
## Introduction
Magento 2, a feature-rich eCommerce platform, provides robust functionalities to online retailers through its versatile modules and customization options. A key aspect of Magento's functionality lies in its directory structure, which organizes the various files and directories that make up a Magento 2 site. This document aims to guide you through Magento 2's directory structure, helping you navigate and understand the system's intricacies.


<a href="#overview"></a>
## Overview

When you first install Magento 2, the root directory will be structured as follows:

```
magento2/
├── app/
├── bin/
├── dev/
├── generated/
├── lib/
├── pub/
├── setup/
├── var/
├── vendor/
└── .htaccess
```
These directories each play a specific role in Magento 2. Let's break down each one in more detail.

## Key Directories

### `app/`

The `app/` directory is one of the most essential directories, containing several important subdirectories:

- `code/`: All the custom modules are located here.
- `design/`: Contains all theme files. It is further divided into frontend and backend themes.
- `etc/`: Holds the main configuration files.
- `i18n/`: Contains localization-related files.

Example:

```bash
app/
├── code/
├── design/
├── etc/
└── i18n/
```

### `bin/`

This directory contains the Magento shell command-line script `magento`.

### `dev/`

The `dev/` directory holds the testing files, such as integration, functional, and static tests.

### `generated/`

In Magento 2, the `generated/` directory is home to the Interception Cache classes, which are auto-generated classes forming part of Magento's object management system.

### `lib/`

The `lib/` directory holds the Magento 2 core library files, as well as other third-party libraries that aren't composer packages.

### `pub/`

The `pub/` directory is the Magento 2 root, and it serves static files and media. It's also where the `.htaccess` file lives to protect against direct file access.

## `pub/media/`

The `pub/media/` directory, nested within the `pub/` directory, is a crucial part of Magento 2's structure. This directory serves as the storage location for all the media files utilized by your Magento 2 installation. Here's a breakdown of what you can typically find within the `pub/media/` directory:

- `catalog/`: This subdirectory contains all the images related to your product catalog. These images are further divided into product and category subfolders, following the pattern `catalog/product` and `catalog/category`.

- `customer/`: Stores profile pictures of customers if your website has such functionality.

- `downloadable/`: If you sell downloadable products, the files that customers download are stored here.

- `import/`: This directory is used to store images that are imported using Magento's import functionality.

- `theme/`: It contains media files related to your Magento 2 themes.

- `captcha/`: Stores the images used for CAPTCHA functionality on your website.

- `tmp/`: As the name suggests, this directory is for temporary storage. Magento uses it to store images temporarily during product imports.

- `wysiwyg/`: This directory stores all the media files uploaded via the WYSIWYG editor in the Magento Admin.

Here's an example structure of `pub/media/`:

```bash
pub/media/
├── catalog/
├── customer/
├── downloadable/
├── import/
├── theme/
├── captcha/
├── tmp/
└── wysiwyg/
```

Remember, you should never manually delete or alter files in the `pub/media/` directory, as this could inadvertently remove images from your site or cause issues with the Magento Media Storage system. Always use Magento's built-in functionalities or your server's file management system when dealing with files in `pub/media/`.

### `setup/`

The `setup/` directory is used for the Magento 2 installation process and updater.

### `var/`

The `var/` directory is where temporary files are stored, such as cache, logs, sessions, and reports.

### `vendor/`

The `vendor/` directory is where Composer-managed dependencies reside. Any modules, themes, or libraries that are added via Composer will be placed in this directory.

## .htaccess

The `.htaccess` file manages server configurations such as URL rewrites, SSL certificates, and access control.

## Conclusion

Understanding Magento 2's directory structure is crucial for effective Magento development and customization. This structure ensures that each piece of Magento functionality has its place, making it easier for developers to navigate and modify the system.

Remember to handle these directories carefully, particularly when installing extensions or performing updates. Missteps can lead to significant functionality problems. Good luck with your Magento 2 development!
