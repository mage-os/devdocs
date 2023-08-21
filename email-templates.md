# Email Templates Documentation

[TOC]

## Introduction

Email templates are an essential part of any application that requires sending automated emails. In the context of
Magento 2, email templates play a crucial role in providing a standardized format for sending transactional emails to
customers, such as order confirmation, shipment details, and password reset notifications. This documentation aims to
guide developers on how to create and customize email templates in Magento 2 using PHP.

## 1. Creating Email Templates <a name="creating-email-templates"></a>

Magento 2 provides a straightforward way to create email templates. These templates define the structure and content of
the email being sent. Email templates are stored in the `app/design/frontend/{Vendor}/{Theme}/Magento_Email/email/`
directory of your Magento installation.

To create a new email template, follow these steps:

1. In your theme directory, create the `email` directory if it doesn't already exist.
2. Create a new `.html` file corresponding to the email template you want to create. For
   example, `order_confirmation.html` for the order confirmation email.
3. Open the file and define the HTML structure of your email. You can use inline CSS or include external CSS files.
4. Add placeholders using the following syntax: `{{var placeholder_name}}`. These placeholders will be replaced with
   dynamic content when the email is sent.

Example of a basic email template:

```html
<!-- app/design/frontend/{Vendor}/{Theme}/Magento_Email/email/order_confirmation.html -->

<!-- HTML structure of the email -->
<html>
<body>
<h1>Order Confirmation</h1>
<p>Dear {{var customer_name}},</p>
<p>Your order {{var order_increment_id}} has been confirmed.</p>
</body>
</html>
```

## 2. Customizing Email Templates <a name="customizing-email-templates"></a>

Magento 2 allows you to customize the existing email templates or create new ones based on your specific requirements.
To customize an email template:

1. Identify the email template you wish to modify. Magento provides a list of predefined templates, such
   as `sales_email_order_template`, `sales_email_shipment_template`, etc.
2. In your theme directory, create the `email` directory if it doesn't already exist.
3. Copy the desired email template file from `vendor/magento/module-email/view/frontend/email/`
   to `app/design/frontend/{Vendor}/{Theme}/Magento_Email/email/`.
4. Modify the copied email template as per your requirements.

Example of customizing an existing email template:

```html
<!-- app/design/frontend/{Vendor}/{Theme}/Magento_Email/email/sales_email_order_template.html -->

<!-- Customized email template -->
<html>
<body>
<h1>New Order Notification</h1>
<p>Dear Admin,</p>
<p>A new order has been placed with the following details:</p>

<!-- Custom logic to display additional order details -->
<p>Order ID: {{var order.increment_id}}</p>
<p>Order Total: {{var order.base_grand_total}}</p>

<p>Please take appropriate action.</p>
</body>
</html>
```

## 3. Variables and Conditions <a name="variables-and-conditions"></a>

Email templates in Magento 2 can utilize variables and conditions to dynamically populate content and control the flow
of the email. These variables provide access to various data associated with the email, such as customer information,
order details, etc.

To use variables and conditions, wrap them in double curly braces (`{{ }}`). For example, `{{var customer_name}}` is a
variable that will be replaced with the actual customer name when the email is sent.

Example of using variables and conditions in an email template:

```html
<!-- app/design/frontend/{Vendor}/{Theme}/Magento_Email/email/order_confirmation.html -->

<html>
<body>
<h1>Order Confirmation</h1>

<!-- Conditionally display a personalized greeting -->
{{if customer.is_logged_in}}
<p>Dear {{var customer_name}},</p>
{{else}}
<p>Dear Valued Customer,</p>
{{/if}}

<p>Your order {{var order_increment_id}} has been confirmed.</p>

<!-- Display order items using a loop -->
<table>
    <tr>
        <th>Product</th>
        <th>Price</th>
    </tr>
    {{foreach order.getItems() as item}}
    <tr>
        <td>{{var item.name}}</td>
        <td>{{var item.price}}</td>
    </tr>
    {{/foreach}}
</table>

</body>
</html>
```

## 4. Rendering Email Templates <a name="rendering-email-templates"></a>

Once you have created or customized an email template, you need to render it within your code to send the email. In
Magento 2, you can render email templates using the `Magento\Framework\Mail\Template\TransportBuilder` class.

Example of rendering and sending an email using a custom template:

```php
<?php

use Magento\Framework\App\Area;
use Magento\Framework\Mail\Template\TransportBuilder;
use Magento\Framework\App\ObjectManager;
use Magento\Store\Model\StoreManagerInterface;

class EmailSender
{
    private $transportBuilder;
    private $storeManager;
    
    public function __construct(
        TransportBuilder $transportBuilder,
        StoreManagerInterface $storeManager
    ) {
        $this->transportBuilder = $transportBuilder;
        $this->storeManager = $storeManager;
    }
    
    public function sendOrderConfirmationEmail($customerEmail, $order)
    {
        $templateOptions = [
            'area' => Area::AREA_FRONTEND,
            'store' => $this->storeManager->getStore()->getId()
        ];
        
        $templateVars = [
            'order' => $order,
            'customer' => [
                'is_logged_in' => true,
                'name' => 'John Doe'
            ]
        ];
        
        $from = [
            'email' => 'sender@example.com',
            'name' => 'Sender Name'
        ];
        
        $this->transportBuilder->setTemplateIdentifier('order_confirmation')
            ->setTemplateOptions($templateOptions)
            ->setTemplateVars($templateVars)
            ->setFrom($from)
            ->addTo($customerEmail)
            ->getTransport()
            ->sendMessage();
    }
}

```

## 5. Conclusion <a name="conclusion"></a>

Email templates in Magento 2 are powerful tools for creating standard email formats and customizing their content. By
following the instructions provided in this documentation, you can create, customize, and render email templates that
meet your specific requirements. Remember to utilize variables and conditions to dynamically populate content and
control the flow of your emails. Happy coding!
