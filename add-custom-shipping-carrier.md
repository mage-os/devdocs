---
description: Find out how to integrate custom shipping carriers into Mage-OS. Configure new shipping options tailored to your business needs, enhancing your eCommerce platform’s flexibility and functionality.
keywords: Mage-OS, Mage-OS custom shipping, add shipping carrier, custom shipping method, shipping integration, Mage-OS shipping configuration, Magento carrier setup, Magento shipping module
communityNote: false
---
# Add custom shipping carrier

[TOC]

Mage-OS allows the creation of custom shipping carriers to handle various shipping methods for
different carriers or logistics providers. A custom shipping carrier can be added by creating a
Mage-OS module and configuring the required fields to handle shipping calculations,
carrier configurations, and frontend integration.

## Module Setup

The first step in adding a custom shipping carrier is creating the necessary directory structure
for the Mage-OS module:

```bash
app/code/MageOS/ShippingCarrier/
├── registration.php
├── composer.json
├── etc
│   ├── module.xml
│   ├── config.xml
│   ├── adminhtml
        └── system.xml
├── Model
│   └── Carrier
│       └── CustomCarrier.php
```

Create register module file `app/code/MageOS/ShippingCarrier/registration.php`

```php
<?php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Vendor_ShippingCarrier',
    __DIR__
);
```

Next, you need to declare your module in `app/code/MageOS/ShippingCarrier/etc/module.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="MageOS_ShippingCarrier"/>
</config>
```

## Shipping Carrier Configuration

In the `config.xml` file, define the shipping carrier's core settings, such as its active state,
title, and allowed countries. Create `app/code/MageOS/ShippingCarrier/etc/config.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Shipping/etc/config.xsd">
    <default>
        <carriers>
            <customcarrier>
                <active>1</active>
                <title>Custom Shipping Carrier</title>
                <name>Custom Shipping Method Name</name>
                <shipping_cost>10</shipping_cost>
                <sallowspecific>0</sallowspecific>
                <sort_order>15</sort_order>
                <model>MageOS\ShippingCarrier\Model\Carrier\CustomCarrier</model>
            </customcarrier>
        </carriers>
    </default>
</config>
```

Explanation:

- active: Enables or disables the custom carrier.
- title: The name displayed in the checkout.
- name: Internal name of the carrier.
- model: The path to the custom shipping carrier model.
- shipping_cost: The amount of the handling fee.

## Admin Configuration for Carrier

To allow store administrators to configure the shipping method, we define settings in
`app/code/MageOS/ShippingCarrier/etc/adminhtml/system.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Config:etc/system_file.xsd">
    <system>
        <section id="carriers">
            <group id="customcarrier" translate="label" type="text" sortOrder="0" showInDefault="1" showInWebsite="1" showInStore="1">
                <label>Custom Shipping Module</label>
                <field id="active" translate="label" type="select" sortOrder="10" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Enabled</label>
                    <source_model>Magento\Config\Model\Config\Source\Yesno</source_model>
                </field>
                <field id="title" translate="label" type="text" sortOrder="20" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Title</label>
                </field>
                <field id="name" translate="label" type="text" sortOrder="30" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Method Name</label>
                </field>
                <field id="shipping_cost" translate="label" type="text" sortOrder="40" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Shipping Cost</label>
                    <validate>validate-number validate-zero-or-greater</validate>
                </field>
                <field id="sallowspecific" translate="label" type="select" sortOrder="50" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Ship to Applicable Countries</label>
                    <frontend_class>shipping-applicable-country</frontend_class>
                    <source_model>Magento\Shipping\Model\Config\Source\Allspecificcountries</source_model>
                </field>
                <field id="specificcountry" translate="label" type="multiselect" sortOrder="60" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Ship to Specific Countries</label>
                    <source_model>Magento\Directory\Model\Config\Source\Country</source_model>
                    <can_be_empty>1</can_be_empty>
                </field>
                <field id="showmethod" translate="label" type="select" sortOrder="70" showInDefault="1" showInWebsite="1" showInStore="1">
                    <label>Show Method if not applicable</label>
                    <source_model>Magento\Config\Model\Config\Source\Yesno</source_model>
                    <frontend_class>shipping-skip-hide</frontend_class>
                </field>
                <field id="sort_order" translate="label" type="text" sortOrder="80" showInDefault="1" showInWebsite="1" showInStore="1" canRestore="1">
                    <label>Sort Order</label>
                </field>
            </group>
        </section>
    </system>
</config>
```

This configuration allows administrators to enable the carrier, set a title, and configure a handling
fee through the Mage-OS admin panel.

## Shipping Carrier Model

The core logic for the custom shipping carrier is in the CustomCarrier.php model.
This class extends Mage-OS's abstract shipping carrier class and implements the shipping calculation and rates.

```php
<?php
declare(strict_types=1);

namespace MageOS\ShippingCarrier\Model\Carrier;

use Magento\Framework\App\Config\ScopeConfigInterface;
use Magento\Quote\Model\Quote\Address\RateRequest;
use Magento\Quote\Model\Quote\Address\RateResult\Method;
use Magento\Quote\Model\Quote\Address\RateResult\MethodFactory;
use Magento\Quote\Model\Quote\Address\RateResult\ErrorFactory;
use Magento\Shipping\Model\Carrier\AbstractCarrier;
use Magento\Shipping\Model\Carrier\CarrierInterface;
use Magento\Shipping\Model\Rate\Result;
use Magento\Shipping\Model\Rate\ResultFactory;
use Psr\Log\LoggerInterface;

class CustomCarrier extends AbstractCarrier implements CarrierInterface
{
    protected $_code = 'customcarrier';

    protected $_isFixed = true;

    private ResultFactory $rateResultFactory;

    private MethodFactory $rateMethodFactory;

    public function __construct(
        ScopeConfigInterface $scopeConfig,
        ErrorFactory $rateErrorFactory,
        LoggerInterface $logger,
        ResultFactory $rateResultFactory,
        MethodFactory $rateMethodFactory,
        array $data = []
    ) {
        parent::__construct($scopeConfig, $rateErrorFactory, $logger, $data);

        $this->rateResultFactory = $rateResultFactory;
        $this->rateMethodFactory = $rateMethodFactory;
    }

    /**
     * Custom Shipping Rates Collector
     *
     * @param RateRequest $request
     * @return \Magento\Shipping\Model\Rate\Result|bool
     */
    public function collectRates(RateRequest $request)
    {
        if (!$this->getConfigFlag('active')) {
            return false;
        }

        /** @var Method $method */
        $method = $this->rateMethodFactory->create();

        $method->setCarrier($this->_code);
        $method->setCarrierTitle($this->getConfigData('title'));

        $method->setMethod($this->_code);
        $method->setMethodTitle($this->getConfigData('name'));

        $shippingPrice = (float)$this->getConfigData('shipping_cost');
        $method->setPrice($shippingPrice);
        $method->setCost($shippingPrice);
        $method->setDataUsingMethod('cost', $shippingPrice);

        /** @var Result $result */
        $result = $this->rateResultFactory->create();
        $result->append($method);

        return $result;
    }

    public function getAllowedMethods(): array
    {
        return [$this->_code => $this->getConfigData('name')];
    }
}
```

Explanation:

- collectRates(): Calculates shipping rates based on the quote request and returns them.
  Here, a fixed rate of 10.00 is used.
- getAllowedMethods(): Returns the allowed shipping methods for this carrier.

## Frontend Integration

Once the backend logic is in place, the custom shipping carrier will automatically appear in the Mage-OS checkout
if it's enabled and configured properly. The title and price will be displayed as defined in the carrier configuration.

## Conclusion
This guide walks through the basic setup of a custom shipping carrier in Mage-OS. The carrier integrates with Mage-OS’s shipping framework, allowing you to customize the shipping calculation and display it during the checkout process. You can extend this basic structure to integrate with third-party APIs, offer dynamic shipping rates, or introduce more complex shipping logic based on cart contents or customer information.
