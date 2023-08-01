# Magento 2 Security Features Documentation

[TOC]

## Introduction

Welcome to the documentation for security features in Magento 2! This guide will provide you with essential information
on how to secure your Magento 2 installation. It covers various security features and best practices that will help
protect your Magento store from potential threats.

## Secure Configuration

### File Permissions

File permissions play a vital role in protecting your Magento installation. Ensure that all directories have the
appropriate permissions. For example, directories should have a permission of 755, and files should have a permission of
644. Restricting write permissions only to necessary files and directories is crucial to prevent unauthorized
modifications.

```bash
find . -type f -exec chmod 644 {} \;
find . -type d -exec chmod 755 {} \;
```

### Secure Admin Panel

To secure your admin panel, change the default URL path from `/admin` to a custom one. You can achieve this by modifying
the `admin/url/custom` configuration option in the `app/etc/env.php` file.

```php
'backend' => [
    'frontName' => 'your_custom_admin_path'
],
```

Additionally, use strong usernames and passwords for admin accounts and enforce regular password changes. Restrict
access to the admin panel to specific IP addresses using `.htaccess` or server configuration files.

### Enable Two-Factor Authentication

Enable two-factor authentication (2FA) for admin users to provide an extra layer of security. Magento 2 supports
multiple 2FA providers, such as Google Authenticator and Duo Security. Admin users can enable 2FA from their account
settings in the admin panel.

## Secure Coding Practices

### Input Validation

Always validate user inputs to prevent potential security vulnerabilities, such as cross-site scripting (XSS) attacks
and SQL injections. Use Magento's built-in validation methods, such as `escapeHtml` or `validate-data`, to sanitize and
validate user inputs before processing them.

```php
$validatedValue = $this->escapeHtml($value);
```

### Cross-Site Scripting (XSS) Prevention

To prevent cross-site scripting attacks, make sure to escape user-generated content before displaying it in HTML
templates or JavaScript. Magento provides different methods like `escapeHtml`, `escapeJs`, or `escapeUrl` to properly
sanitize user data.

```php
$escapedContent = $this->escapeHtml($content);
```

### SQL Injection Prevention

When interacting with databases, always use Magento's built-in methods to prepare and execute SQL queries. This will
help prevent SQL injection attacks by automatically escaping user inputs.

```php
$connection = $this->resourceConnection->getConnection();
$query = $connection->select()->from('table')->where('column = ?', $value);
```

### Secure Password Storage

Ensure that passwords are securely stored by using Magento's password hashing methods. Never store plain text passwords
in your database. Magento 2's password hashing algorithm uses bcrypt with a salt, which provides a strong level of
security.

```php
$hash = $this->encryptor->getHash($password);
if ($this->encryptor->validateHash($password, $hash)) {
    // Password is valid
}
```

## Secure File Handling

### File Uploads

Validate and sanitize file uploads to prevent potential security risks. Use Magento's built-in file validation methods,
such as `isValid`, to ensure that uploaded files meet your requirements. Also, consider storing uploaded files outside
of the web root directory to prevent direct access.

```php
$fileUploader = $this->fileUploaderFactory->create(['fileId' => 'file']);
if ($fileUploader->isValid()) {
    $fileUploader->save('path/to/save');
}
```

### File Inclusion

Avoid using user inputs directly in file inclusion functions to prevent directory traversal and remote file inclusion
attacks. Always validate and sanitize user inputs before using them in file inclusion operations.

```php
$validatedFileName = $this->escapeHtml($fileName);
include 'path/to/files/' . $validatedFileName;
```

### File Download

When providing file downloads to users, ensure that sensitive files are not accessible to unauthorized users. Implement
proper authentication and authorization checks before allowing file downloads.

## User Authentication and Authorization

### Password Policies

Enforce strong password policies for all user accounts. Require password complexity, such as minimum length, the use of
alphanumeric characters, and a mix of upper and lowercase letters. Periodically prompt users to change their passwords
to enhance security.

### Role-Based Access Control

Implement role-based access control (RBAC) to grant appropriate permissions to users based on their roles. Magento 2
provides a robust RBAC system that allows you to define roles and assign permissions to restrict access to certain areas
and resources.

### Secure Session Management

Ensure secure session management by using secure cookies, enabling secure session options, and enforcing session
timeouts. Make sure to set the `cookie_secure` and `cookie_httponly` options to `true` in your Magento configuration.

## Secure Communication

### HTTPS Configuration

Configure your Magento installation to use HTTPS for all communication to ensure secure data exchange between clients
and the server. Obtain and install a valid SSL certificate and configure your web server accordingly.

### Secure APIs

When developing custom APIs, ensure that they are properly secured. Use OAuth or token-based authentication to protect
API endpoints and validate user access. Implement rate limiting and consider using API gateways for additional security.

### Secure Payment Gateways

When integrating payment gateways, choose trusted providers that adhere to PCI DSS (Payment Card Industry Data Security
Standard) compliance. Implement secure payment methods, such as tokenization, to prevent storing sensitive payment
information in your database.

## Conclusion

Congratulations! You have now learned about various security features and best practices to secure your Magento 2
installation. By implementing these measures, you can protect your online store from potential security threats and
ensure a safe shopping experience for your customers. Remember to keep your Magento installation updated with the latest
security patches and follow Magento's security guidelines to stay ahead of evolving security risks.
