# Add custom shipping carrier

[TOC]

Magento 2 allows the creation of custom shipping carriers to handle various shipping methods for different carriers or logistics providers. A custom shipping carrier can be added by creating a Magento 2 module and configuring the required fields to handle shipping calculations, carrier configurations, and frontend integration.

## Module Setup

The first step in adding a custom shipping carrier is creating the necessary directory structure for the Mage-OS module:

```bash
app/code/Vendor/ShippingCarrier/
├── registration.php
├── etc
│   ├── module.xml
│   ├── config.xml
│   ├── system.xml
├── Model
│   └── Carrier
│       └── CustomCarrier.php
```

Create register module file `app/code/Vendor/ShippingCarrier/registration.php`
```php
<?php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Vendor_ShippingCarrier',
    __DIR__
);
```

Next, you need to declare your module in `app/code/Vendor/ShippingCarrier/etc/module.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Vendor_ShippingCarrier" />
</config>
```

## Shipping Carrier Configuration

In the `config.xml` file, define the shipping carrier's core settings, such as its active state, title, and allowed countries. Create `app/code/Vendor/ShippingCarrier/etc/config.xml`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Shipping/etc/config.xsd">
    <default>
        <carriers>
            <customcarrier>
                <active>1</active>
                <title>Custom Shipping Carrier</title>
                <name>Custom Carrier</name>
                <allowspecific>0</allowspecific> <!-- Set to 1 to limit specific countries -->
                <specificcountry>US,CA</specificcountry> <!-- Countries where shipping method is allowed -->
                <model>Vendor\ShippingCarrier\Model\Carrier\CustomCarrier</model>
                <handling_type>F</handling_type> <!-- Fixed handling fee -->
                <handling_fee>10.00</handling_fee>
                <sallowspecific>0</sallowspecific>
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
- handling_type: Type of handling fee (F for fixed or P for percent).
- handling_fee: The amount of the handling fee.

# Admin Configuration for Carrier

To allow store administrators to configure the shipping method, we define settings in `app/code/Vendor/ShippingCarrier/etc/adminhtml/system.xml.`:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Backend/etc/system_file.xsd">
    <system>
        <section id="carriers">
            <group id="customcarrier" translate="label" type="text" sortOrder="30" showInDefault="1" showInWebsite="1" showInStore="1">
                <label>Custom Shipping Carrier</label>
                <field id="active" translate="label" type="select" sortOrder="1" showInDefault="1" showInWebsite="1" showInStore="1">
                    <label>Enable</label>
                    <source_model>Magento\Config\Model\Config\Source\Yesno</source_model>
                </field>
                <field id="title" translate="label" type="text" sortOrder="2" showInDefault="1" showInWebsite="1" showInStore="1">
                    <label>Title</label>
                </field>
                <field id="handling_fee" translate="label" type="text" sortOrder="5" showInDefault="1" showInWebsite="1" showInStore="1">
                    <label>Handling Fee</label>
                </field>
            </group>
        </section>
    </system>
</config>
```

This configuration allows administrators to enable the carrier, set a title, and configure a handling fee through the Mage-OS admin panel.

# Shipping Carrier Model

The core logic for the custom shipping carrier is in the CustomCarrier.php model. This class extends Mage-OS's abstract shipping carrier class and implements the shipping calculation and rates.

```php
<?php
namespace Vendor\ShippingCarrier\Model\Carrier;

use Magento\Shipping\Model\Carrier\AbstractCarrier;
use Magento\Shipping\Model\Carrier\CarrierInterface;
use Magento\Quote\Model\Quote\Address\RateRequest;
use Magento\Shipping\Model\Rate\Result;

class CustomCarrier extends AbstractCarrier implements CarrierInterface
{
    protected $_code = 'customcarrier';

    public function collectRates(RateRequest $request)
    {
        if (!$this->getConfigFlag('active')) {
            return false;
        }

        /** @var \Magento\Shipping\Model\Rate\Result $result */
        $result = $this->_rateResultFactory->create();

        // Set shipping cost
        $shippingPrice = 10.00;

        /** @var \Magento\Quote\Model\Quote\Address\RateResult\Method $method */
        $method = $this->_rateMethodFactory->create();
        $method->setCarrier($this->_code);
        $method->setCarrierTitle($this->getConfigData('title'));

        $method->setMethod($this->_code);
        $method->setMethodTitle('Custom Carrier Method');

        $method->setPrice($shippingPrice);
        $method->setCost($shippingPrice);

        $result->append($method);

        return $result;
    }

    public function getAllowedMethods()
    {
        return [$this->_code => $this->getConfigData('name')];
    }
}

```

Explanation:

- collectRates(): Calculates shipping rates based on the quote request and returns them. Here, a fixed rate of 10.00 is used.
- getAllowedMethods(): Returns the allowed shipping methods for this carrier.

# Frontend Integration

Once the backend logic is in place, the custom shipping carrier will automatically appear in the Mage-OS checkout if it's enabled and configured properly. The title and price will be displayed as defined in the carrier configuration.

# Conclusion
This guide walks through the basic setup of a custom shipping carrier in Mage-OS. The carrier integrates with Mage-OS’s shipping framework, allowing you to customize the shipping calculation and display it during the checkout process. You can extend this basic structure to integrate with third-party APIs, offer dynamic shipping rates, or introduce more complex shipping logic based on cart contents or customer information.