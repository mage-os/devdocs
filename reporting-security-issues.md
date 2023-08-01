# Reporting Security Issues

[TOC]

Thank you for your interest in improving the security of PHP and Magento 2. We highly appreciate your efforts in
reporting any security vulnerabilities you may come across. Your contribution helps us ensure the safety and integrity
of our software.

## Security Vulnerabilities

A security vulnerability refers to a weakness or flaw in software that can be exploited by attackers to compromise the
system's confidentiality, integrity, or availability. Examples of security vulnerabilities could include cross-site
scripting (XSS), SQL injection, remote code execution, or insecure direct object references.

## Responsible Disclosure

We strongly encourage responsible disclosure of any security vulnerabilities you discover. This means that you should
not publicly disclose the details of a vulnerability until it has been resolved. Instead, we kindly ask you to report
the issue directly to us so that we can investigate and take necessary actions to protect our users.

## Reporting Process

To report a security issue, please follow these steps:

1. **Gather Information**: Collect as much information as possible about the vulnerability you have discovered. Include
   a detailed description of the issue, along with any steps or code snippets needed to reproduce it. This information
   will help us understand and address the problem more efficiently.

2. **Contact Us**: Send an email to our dedicated security team at security@example.com. Include the subject line "
   Security Vulnerability Report" to ensure prompt attention. In your email, provide a clear and concise explanation of
   the vulnerability, including any relevant supporting materials or code samples.

3. **Encryption**: Please encrypt your email using our [PGP key](https://example.com/security/pgp-key.asc) to protect
   the confidentiality of the information you are sharing. This step ensures that only authorized recipients can access
   the contents of your report.

4. **Response**: Our security team will acknowledge receipt of your report within 24 hours. We will then begin
   investigating the issue and keeping you informed about our progress. Once we have resolved the vulnerability, we will
   notify you and provide credit for your responsible disclosure if desired.

## Vulnerability Examples

Here are a couple of examples to illustrate what we consider a well-written vulnerability report.

### Example 1: Cross-Site Scripting (XSS)

**Description**: A persistent cross-site scripting vulnerability was discovered in the `customer_name` field of the
checkout form. By injecting malicious JavaScript code, an attacker could execute arbitrary code in the context of the
victim's browser.

**Steps to Reproduce**:

1. Log in as a customer with the role of "registered user."
2. Add an item to your cart and proceed to the checkout page.
3. In the `customer_name` field, enter the following payload: `<script>alert('XSS vulnerability');</script>`
4. Complete the checkout process and observe that the payload is executed when viewing the order details.

**Impact**: This vulnerability allows an attacker to execute arbitrary code on the victim's browser, potentially leading
to session hijacking, data theft, or unauthorized actions on the affected website.

### Example 2: SQL Injection

**Description**: A time-based blind SQL injection vulnerability was identified in the `getProductById()` function of
the `ProductRepository` class. By manipulating the `productId` parameter, an attacker can extract sensitive information
from the database.

**Steps to Reproduce**:

1. Retrieve the product details by calling the `getProductById()` function with the following
   payload: `1 OR SLEEP(5) --`
2. Observe that the response is delayed by approximately 5 seconds, indicating a successful time-based injection.

**Impact**: Successful exploitation of this vulnerability allows an attacker to retrieve sensitive information from the
database, such as customer records, order details, or other confidential data.

## Conclusion

We appreciate your commitment to improving the security of PHP and Magento 2. By responsibly disclosing any
vulnerabilities you discover, you contribute to the ongoing protection of our users and maintain the integrity of our
software. Thank you for your cooperation, and we look forward to working with you to address any security concerns.
