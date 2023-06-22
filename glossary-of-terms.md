- [A](#A)
  - [above the fold](#above the fold)
  - [active branch](#active branch)
  - [adapter](#adapter)
  - [admin](#admin)
  - [Admin area](#Admin area)
  - [ADMIN variables](#ADMIN variables)
  - [adminhtml](#adminhtml)
  - [area](#area)
  - [attribute](#attribute)
  - [attribute group](#attribute group)
  - [attribute set](#attribute set)
  - [average inventory cost](#average inventory cost)
- [B](#B)
  - [base currency](#base currency)
  - [batch processing](#batch processing)
  - [block](#block)
  - [brand](#brand)
  - [brick-and-mortar](#brick-and-mortar)
  - [bulk operations](#bulk operations)
  - [bundle product](#bundle product)
  - [bundled extension](#bundled extension)
- [C](#C)
  - [cache backend](#cache backend)
  - [cache frontend](#cache frontend)
  - [cache type](#cache type)
  - [capture](#capture)
  - [cardholder](#cardholder)
  - [cart rules](#cart rules)
  - [catalog](#catalog)
  - [catalog rules](#catalog rules)
  - [category](#category)
  - [checkout](#checkout)
  - [cloud variables](#cloud variables)
  - [CMS block](#CMS block)
  - [complex data](#complex data)
  - [component](#component)
  - [configurable product](#configurable product)
  - [conversion rate](#conversion rate)
  - [core tier scaling](#core tier scaling)
  - [credit memo](#credit memo)
  - [credit memo comment](#credit memo comment)
  - [credit memo item](#credit memo item)
  - [cross-sell](#cross-sell)
  - [CVM](#CVM)
- [D](#D)
  - [database schema](#database schema)
  - [dependency injection](#dependency injection)
  - [deploy key](#deploy key)
  - [double opt-in](#double opt-in)
  - [downloadable product](#downloadable product)
  - [dynamic content](#dynamic content)
  - [dynamic media URL](#dynamic media URL)
- [E](#E)
  - [ece-tools package](#ece-tools package)
  - [entity](#entity)
  - [entity attribute value](#entity attribute value)
  - [evergreen content](#evergreen content)
  - [extension](#extension)
  - [extension attribute](#extension attribute)
- [F](#F)
  - [freight on board](#freight on board)
  - [frontend](#frontend)
  - [frontend properties](#frontend properties)
  - [fulfillment](#fulfillment)
- [G](#G)
  - [gift card](#gift card)
  - [gross margin](#gross margin)
  - [grouped product](#grouped product)
- [H](#H)
  - [handle](#handle)
  - [horizontal scaling](#horizontal scaling)
- [I](#I)
  - [interception](#interception)
- [L](#L)
  - [layout](#layout)
  - [layout instructions](#layout instructions)
  - [layout update](#layout update)
  - [License Owner](#License Owner)
- [M](#M)
  - [MAGEID](#MAGEID)
  - [markup](#markup)
  - [master environment](#master environment)
  - [merchant account](#merchant account)
  - [MFTF](#MFTF)
  - [module](#module)
- [O](#O)
  - [OMS](#OMS)
  - [origin cloaking](#origin cloaking)
- [P](#P)
  - [Page Builder](#Page Builder)
  - [payment gateway](#payment gateway)
- [R](#R)
  - [related product](#related product)
- [S](#S)
  - [sales rules](#sales rules)
  - [scope](#scope)
  - [service contract](#service contract)
  - [settlement](#settlement)
  - [Shared Catalog](#Shared Catalog)
  - [shipment](#shipment)
  - [shipment document](#shipment document)
  - [shipping carrier](#shipping carrier)
  - [shopping cart](#shopping cart)
  - [simple product](#simple product)
  - [SKU](#SKU)
  - [splash page](#splash page)
  - [static block](#static block)
  - [static content](#static content)
  - [static files](#static files)
  - [store](#store)
  - [store view](#store view)
  - [storefront](#storefront)
- [T](#T)
  - [tax rule](#tax rule)
  - [template](#template)
  - [theme](#theme)
- [U](#U)
  - [UI component](#UI component)
  - [UPWARD](#UPWARD)
- [V](#V)
  - [Vendor Bundled Extension](#Vendor Bundled Extension)
  - [vertical scaling](#vertical scaling)
  - [virtual product](#virtual product)
  - [virtual type](#virtual type)
- [W](#W)
  - [website](#website)
  - [widget](#widget)


<a href="#A"></a>
## A
<a href="#above the fold"></a>
### above the fold
In a browser window, the content that is immediately visible after a web page loaded and before a user scrolled down the page.
When designing your layout, use flexible formats to best display the highest priority products, features, sales, notifications, options, and so on, in this area.
With mobile and tablets, the area of above the fold greatly differs, especially on the size and dimensions of the screen and orientation when viewing (portrait vs landscape).
Using responsive themes and testing can help find the right mix of content and layout.

<a href="#active branch"></a>
### active branch
An active branch or environment is one that is connected to a deployed or running instance with access to services.
When you deactivate, the connection to the services and to the running instance is removed, but the code is preserved.
It becomes an ordinary git branch.

<a href="#adapter"></a>
### adapter
A class that enables two otherwise incompatible systems to work together without modifying the systems’ source code.
Examples include database adapters, cache adapters, filesystem adapters, post-processor libraries adapters, and other types of computing adapters.

<a href="#admin"></a>
### admin
In software, a user role with full administrator privileges to manage all functionality.
In Mage-OS, admin users have full permissions and access to all features, options, and capabilities in the Admin.
They can also create users and roles.

<a href="#Admin area"></a>
### Admin area
The password-protected back office of your store where orders, catalog, content, and configurations are managed.
Users access the Admin area to manage the store, including products, orders, shipments, CMS content, design of the storefront, customer information, and so on.
Admin users have an associated role with permissions that controls access to features, options, and capabilities.

<a href="#ADMIN variables"></a>
### ADMIN variables
ADMIN variables are project environment variables to override the configuration settings for the Admin user account to access the Admin UI.

<a href="#adminhtml"></a>
### adminhtml
The internal area name assigned to the Admin.

<a href="#area"></a>
### area
Area is an abstract term for a Mage-OS application scope.
Areas are logical components that organize code for optimized request processing.
Areas reduce the memory demands of configuration objects accessed from the storefront, and they streamline web service calls by loading only the required dependent code.
Each area can contain completely different code to process URLs and requests.

<a href="#attribute"></a>
### attribute
A characteristic or property of a product that describes some aspect of the product.
Mage-OS or Mage-OS Open Source users can create custom attributes to add to the default attribute set or a custom attribute set.
Create these attributes through the Admin or programmatically.
Examples: color, size, weight, price, age, gender, and so on.
Custom attributes are a type of Entity-Attribute-Value (EAV) attribute.
For integrations like Google Shopping ads Channel and Amazon Sales Channel, you map Commerce attributes to attributes in the third-party to properly display and sell products, display ads.

<a href="#attribute group"></a>
### attribute group
A logical grouping of attributes within an attribute set.

<a href="#attribute set"></a>
### attribute set
A collection of attribute groups, customized for a specific product.
Example: A T-shirt attribute set might include color, size, gender, and brand.

<a href="#average inventory cost"></a>
### average inventory cost
Product price, less coupons, or discounts, plus freight and applicable taxes.
The average is determined by adding the beginning cost of inventory each month, plus the ending cost of inventory for the last month of the period.

<a href="#B"></a>
## B
<a href="#base currency"></a>
### base currency
The primary currency that is used per store view for all online payments.
Stores can accept currencies from more than 200 countries around the world.
The store front provides a currency selector for multiple accepted currencies for a specific country or locale.
Currency symbols appear in product prices and sales documents such as orders and invoices.
You can customize the currency symbols as needed and set the display of the price separately for each store or view.

<a href="#batch processing"></a>
### batch processing
To perform a task or change multiple items all at once, without manual repetition.

<a href="#block"></a>
### block
A unit of page output that renders some distinctive content - a piece of information, a user interface element - anything visually tangible for the end-user.
Blocks are implemented and provided by modules. Blocks use templates to generate HTML.
Examples of blocks include a category list, a mini cart, product tags, and product listing.
Dynamic blocks provide content based on logic, such as price rules.
Page Builder expands on the interactivity and creation of blocks and dynamic blocks.

<a href="#brand"></a>
### brand
A unique identity that defines a particular product or group of products by the manufacturer or Designer.
These include name brands for clothing, appliances, luxury items, and so on.
Your company may also be the brand, selling products under multiple brands based on the business unit, target audience, and so on.
Use custom attributes to save brand information for products.
Some extensions and integrations may use or require a brand for your products, such as Google Shopping ads Channel and Amazon Sales Channel.

<a href="#brick-and-mortar"></a>
### brick-and-mortar
A retail business with a permanent physical location, as opposed to businesses that function virtually or solely through the internet.
For Inventory Management and Order Management, this store is a source for tracking product quantities, shipping orders, and supporting in-store pickup.

<a href="#bulk operations"></a>
### bulk operations
Bulk operations are actions that are performed on a large scale.
Example bulk operations tasks include importing or exporting items, changing prices on a mass scale, and assigning products to a warehouse.

<a href="#bundle product"></a>
### bundle product
Lets customers assemble a “build your own” customizable product from various options and configurations.
Each item in the bundle is either a separate simple or virtual product.

<a href="#bundled extension"></a>
### bundled extension
The code that extends or customizes Mage-OS behavior is considered a Bundled Extension.
It can include modules, themes, and language packs.

<a href="#C"></a>
## C
<a href="#cache backend"></a>
### cache backend
Stores cache records into a two-level backend system within Zend’s default framework.
A first-level cache is fast — for example, an APC or Memcached backend — but it is limited and does not support tagging and grouping of cache entries.
A second-level cache — for example, a file system or a Redis backend — is slower but supports tagging and grouping.

<a href="#cache frontend"></a>
### cache frontend
Specifies what kind of data is stored in the cache backend.

<a href="#cache type"></a>
### cache type
A cache stores data so that future calls for that data load faster.
Other types can be created and defined.

<a href="#capture"></a>
### capture
The process of converting an authorized order amount into a billable transaction.
Transactions cannot be captured until authorized, and authorizations cannot be captured until the goods or services have been shipped.

<a href="#cardholder"></a>
### cardholder
A person who is authorized by a financial institution to make purchases on a credit card account.

<a href="#cart rules"></a>
### cart rules
Price rules that are applied to the shopping cart and trigger an action in response to a set of conditions.
Used to create promotions.

<a href="#catalog"></a>
### catalog
For merchants, the catalog represents their product inventory.
Within Mage-OS architecture, the catalog consists of categories, products, and product attributes.
Each Commerce store has only one product catalog, which is shared by all store views.
In a multi-store installation, each store can have a separate catalog, or share the catalog.
The current store catalog is determined by the default root category, visible to the user in the top navigation (main menu) of the store.
(The term “root category” may be confusing, because the “root category” isn’t really a category at all, but a container for the menu, which consists of categories and subcategories.)
You can create as many root categories as you want, but only one (the default) can be used at a time.

<a href="#catalog rules"></a>
### catalog rules
Price rules that are applied to specific products and trigger an action in response to a set of conditions.
Used to create promotions.

<a href="#category"></a>
### category
A group of products that have something in common.
The main menu of the store is organized into categories and subcategories of products.

<a href="#checkout"></a>
### checkout
The process of gathering the payment and shipping information that is necessary to complete the purchase of items in the shopping cart.
After the customer reviews the information and submits the order, an email confirmation is sent to the customer.
Checkout has many options and configuration out-of-the-box and through extension.

<a href="#cloud variables"></a>
### cloud variables
Cloud variables are environment variables specific to Mage-OS on cloud infrastructure and use the prefix.

<a href="#CMS block"></a>
### CMS block
A special variant of block that can only be created in the Admin and cannot be referenced through layout files.

<a href="#complex data"></a>
### complex data
Data that is associated with multiple product options.

<a href="#component"></a>
### component
Used to refer to a module, theme, or language package in Mage-OS.

<a href="#configurable product"></a>
### configurable product
A configurable product looks like a single product with drop-down lists of options for each variation.
Each option is actually a separate simple product with a unique SKU, which makes it possible to track inventory for each product variation.
To achieve a similar effect, a simple product can be used with custom options, but without the ability to track inventory for each variation.
Products with multiple options are sometimes referred to as composite products.
Although a configurable product uses more SKUs, and may initially take a little longer to set up, it can save you time in the end.
If you plan to grow your business, the configurable product type might be a better choice for a product with multiple options.
Example: T-shirts that are available in two colors and three sizes.
Six variants must be created as individual products (each with its own SKU).
Then, all variants are added to a configurable product where customers can choose the size and color, and then add it to their cart.

<a href="#conversion rate"></a>
### conversion rate
The percentage of visitors who are converted into buyers.

<a href="#core tier scaling"></a>
### core tier scaling
Core tier scaling consists of three service nodes for data storage, cache and services, such as OpenSearch, Elasticsearch, MariaDB, Redis.

<a href="#credit memo"></a>
### credit memo
A document issued by the merchant to a customer to write off an outstanding balance because of overcharge, rebate, or return of goods.
The memo restores funds to the customer’s account.

<a href="#credit memo comment"></a>
### credit memo comment
Details why a credit memo amount was credited to the customer.

<a href="#credit memo item"></a>
### credit memo item
An invoiced item for which a merchant creates a credit memo.

<a href="#cross-sell"></a>
### cross-sell
A product that appears next to the shopping cart.
When a customer navigates to the shopping cart page, these products are displayed as cross-sells to the items already in the shopping cart.
They are similar to impulse buys, like magazines and candy at the cash registers in grocery stores.

<a href="#CVM"></a>
### CVM
An abbreviation for “Cardholder Verification Method”.
A way to verify the identity of the customer by confirming a 3-digit or 4-digit credit card security code with the payment processor.

<a href="#D"></a>
## D
<a href="#database schema"></a>
### database schema
The structure of data in a database.
Defines how data is organized and how data relationships are governed, including all constraints applied to the data.
A module can contain fragments of the database schema if that module has data that must be stored in the database.

<a href="#dependency injection"></a>
### dependency injection
A software design pattern that allows a class to specify its dependencies without having to construct them.
This class delegates the responsibility of injecting the dependency to the calling class.
Used to make testing easier.
To define dependencies for classes, edit the di.xml configuration file.

<a href="#deploy key"></a>
### deploy key
A deploy key is your project SSH public key and enables read-only or read-write (if enabled) access to a Git repository.

<a href="#double opt-in"></a>
### double opt-in
An email verification process that requires potential subscribers to complete a second step that confirms their intention to subscribe.

<a href="#downloadable product"></a>
### downloadable product
A digitally downloadable product that consists of one or more files that are downloaded, such as an eBook, music, video, software application, or an update.
You can offer an album for sale and sell each song individually.
A downloadable product can deliver an electronic version of your product catalog.
Downloadable files can reside on your server or be provided as URLs to any other server or content delivery network.

<a href="#dynamic content"></a>
### dynamic content
Content that is generated by code rather than read from a static template.
After dynamic content is initially rendered when a user visits a page, sometimes the content can be cached and reused without requiring another dynamic call upon a revisit.

<a href="#dynamic media URL"></a>
### dynamic media URL
A URL address that is generated dynamically by the system to reference an image or other media.
The address links directly to assets stored on a server or a content delivery network.
To use a static URL, change the configuration setting.
However, if dynamic media URLs are included in your catalog when you disable the setting, each reference in your catalog becomes a broken link.
Links can be restored by again enabling dynamic media URLs.
Using dynamic media URLs can affect catalog search performance.
Code format: media url=“path/to/image.jpg”

<a href="#E"></a>
## E
<a href="#ece-tools package"></a>
### ece-tools package
A set of scripts and tools designed to manage and deploy the Commerce application. This package simplifies many Mage-OS on cloud infrastructure processes, including deploying to a Docker environment, managing crons, verifying
project configuration, and applying Adobe patches.

<a href="#entity"></a>
### entity
A unique unit or object in programming.
Contains attributes or parameters that can be modified.
Examples include staging — where an update can change entities such as price rules, products, or categories — and database records — where service contracts include data structures that are sent and received.

<a href="#entity attribute value"></a>
### entity attribute value
For database entities, a data model that efficiently encodes entities.
Stores the entity id, attribute name, and value as a triple, which allows new entity attribute names to be created at any time.
In encoding, the number of attributes that can be used to describe entities can scale extensively, but the number that applies to a given entity is minimized.
This data model is flexible, but can be slow.

<a href="#evergreen content"></a>
### evergreen content
Content that has a long shelf life or content that can be reused.

<a href="#extension"></a>
### extension
Code that extends or customizes Mage-OS behavior.
You can optionally package and distribute an extension on Commerce Marketplace or another extension distribution system.
A Commerce extension can include modules, themes, and language packs.

<a href="#extension attribute"></a>
### extension attribute
Extend functionality and often use more complex data types than custom attributes. These attributes do not appear on the GUI.

<a href="#F"></a>
## F
<a href="#freight on board"></a>
### freight on board
In international shipping, this term means that the receiving party is responsible for the shipping charges.
FOB can be based on the place of origin or destination, and be designated as either freight collect or freight prepaid.

<a href="#frontend"></a>
### frontend
In a client-server application, there is the backend and frontend.
The frontend component, or client, is an interface that enables users to manipulate or interact with the underlying backend code.
Backend code runs on a server.
A user cannot directly access backend code.
A user interacts with the storefront, which in turn uses code running on the Commerce server.
Note: In the past, the storefront has been referred to as the “frontend”, and the Admin has been referred to as the “backend”. This usage is no longer supported.

<a href="#frontend properties"></a>
### frontend properties
Properties that determine the presentation and behavior of an attribute from the standpoint of the customer in your store.

<a href="#fulfillment"></a>
### fulfillment
The process of managing customer shipments.

<a href="#G"></a>
## G
<a href="#gift card"></a>
### gift card
A prepaid card or gift certificate that can be used to make purchases in the store.
Each gift card is assigned a unique code which is entered at checkout.
The value of the gift card is reflected in the gift card account balance.
There are three types of gift cards:

Gift cards are configurable, including options for product eligibility and selection of open or fixed amounts.</li></ul>
A gift card can also be redeemed by the store administrator on customer request when the order is being created in the backend.
Gift cards also help promotions, as store administrators can manually create the gift card accounts in the backend and send the gift card codes to the specific customer segment.
Gift cards can serve as a loyalty program targeted at the most active customers who make numerous purchases from the web store or a specific promotional campaign during the holidays.

<a href="#gross margin"></a>
### gross margin
The difference between the cost and price of a product.

<a href="#grouped product"></a>
### grouped product
A product type with several similar, standalone products grouped on a single page.
Can be offered with variations of a single product or by grouping them by season or theme to create a coordinated set.
Each product can be purchased separately, or as part of the group.
For example, for a knife that is available in four sizes, all four knives can be displayed within a grouped product page.
Customers can select the sizes they want and add them to the cart from this page.

<a href="#H"></a>
## H
<a href="#handle"></a>
### handle
Generally, a handle is a way to reference an object.
In Mage-OS, handles are used in many places, most commonly to identify a page.
For page handles, the handle name is derived from the URL, then used to locate and load the layout files for the referenced page.
For example, in the Customer module, there is a layout file called “view/frontend/layout/checkout_cart_index.xml”.
Here “frontend” is the area name and “checkout_cart_index” is the handle name, both of which are derived from the URL.

<a href="#horizontal scaling"></a>
### horizontal scaling
Horizontal scaling (also known as scaling out) is the process of adding additional nodes or machines to your infrastructure to meet growing demand.

<a href="#I"></a>
## I
<a href="#interception"></a>
### interception
The process of injecting new code before, after, or around an existing public function of a PHP class.
To intercept a function, a plug-in implements the additional code to be invoked.
Plug-ins are associated with interception points by the dependency injection configuration file (di.xml).
If multiple plug-ins are defined on the same function, the dependency injection configuration defines the order in which the plug-ins are invoked, allowing multiple plug-ins to be used without conflict.

<a href="#L"></a>
## L
<a href="#layout"></a>
### layout
In the construction of a Commerce page, a layout is a series of blocks assembled in a hierarchy, representing the structure of the page.
Page layout files focus on the highest level of page structure (header, footer, main content area, left sidebar, and so on).
Layout files then assemble content (blocks) into these different areas on the page.

<a href="#layout instructions"></a>
### layout instructions
Markup in a layout file that describes changes to be applied to a structured element tree of blocks, containers, and UI components.
A single layout file can contain multiple layout instructions.
Layout instructions are encoded in XML in layout files.

<a href="#layout update"></a>
### layout update
Used for snippets of code that are added to modify the XML layout or to import the layout instructions from another file.

<a href="#License Owner"></a>
### License Owner
The License Owner (also known as Account Owner) is the designated person in a business organization that manages payments and other business-related issues for the Mage-OS on cloud infrastructure account.
This person serves as the point of contact with Adobe.
After a business purchases an Mage-OS on cloud infrastructure subscription, initial project and code access is available only to the person designated as the License Owner.

<a href="#M"></a>
## M
<a href="#MAGEID"></a>
### MAGEID
MAGEID is typically the billing contact on the Mage-OS account (and may not be the Project Owner of the Mage-OS on cloud infrastructure project).
For access entitlement to Mage-OS and Mage-OS on cloud infrastructure packages, you must use access keys associated with a MAGEID that has been granted access to those packages.

<a href="#markup"></a>
### markup
In marketing and retail, a percentage added to the cost of an item to determine the retail price.
Configure the markup, or markdown, of a product through product customizable options.
In development, a computer language that controls the processing, presentation, and formatting of text.
Also, markup tags are snippets of code that add functionality or content to a CMS page or block.

<a href="#master environment"></a>
### master environment
On Mage-OS on cloud infrastructure, Pro projects use an active Platform as a Service (PaaS) environment called master that includes a copy of your Production environment database and web server.

<a href="#merchant account"></a>
### merchant account
An account with a bank or financial institution that makes it possible to accept credit card transactions.

<a href="#MFTF"></a>
### MFTF
MFTF is a Functional Testing Framework.
It provides a testing framework for Commerce developers and software engineers, such as QA specialists, PHP developers, and system integrators.
Developers and QA can write tests to attempt user interactions with web applications, verify functionality, and automate regression testing.

<a href="#module"></a>
### module
Code that changes or extends features provided by the Mage-OS application.
A module is contained in a directory structure that contains PHP and XML files (configuration, blocks, controllers, helpers, models, and so on) related to a specific functionality to deliver a distinct collection of product
features.
The purpose of each module is to provide specific product features by implementing new functionality or extending the functionality of other modules.
Each module is designed to function independently, so the inclusion or exclusion of a particular module does not impact the functionality of other modules.
A module can also implement widgets, which are page elements that can be customized by business users in the Admin.
Modules can be disabled or removed without breaking the consistency of the Mage-OS application.
One exception: When the module depends on other modules, which requires disabling or removing the dependent modules.

<a href="#O"></a>
## O
<a href="#OMS"></a>
### OMS
OMS is Adobe’s Order Management System offering.
OMS is a flexible and affordable solution for managing, selling, and fulfilling inventory from any sales channel.
OMS provides a seamless customer experience, which increases sales while reducing costs, and accelerates the time to market.
OMS capabilities include:

<a href="#origin cloaking"></a>
### origin cloaking
Origin cloaking is a security feature that allows Mage-OS on cloud infrastructure to block any non-Fastly traffic to prevent DDoS attacks, going to the cloud infrastructure (origin).

<a href="#P"></a>
## P
<a href="#Page Builder"></a>
### Page Builder
Page Builder is a Commerce extension for creating content-rich pages by dragging and dropping pre-built controls to define custom layouts.
These controls are also known as “content types”.
Merchants can design layouts and pages without coding experience.
Extension support is provided for developers to extend Page Builder.

<a href="#payment gateway"></a>
### payment gateway
A payment gateway is a third-party service that seamlessly processes credit card transactions without the customer leaving the merchant’s site.

<a href="#R"></a>
## R
<a href="#related product"></a>
### related product
A selection of products that is presented as an incentive to purchase additional items.
For example, if the customer is viewing the product page for a camera, the related products might include other comparable cameras, a camera case, and a tripod.

<a href="#S"></a>
## S
<a href="#sales rules"></a>
### sales rules
Includes cart and catalog rules, which are used to price a product for promotions.

<a href="#scope"></a>
### scope
In Mage-OS, scope describes the extent of your store hierarchy that a setting can affect.
Scope can apply to the following:
Within the hierarchy, settings applied at a lower level can override some higher-level settings.

<a href="#service contract"></a>
### service contract
A set of PHP interfaces that are defined for a module.
A service contract includes data interfaces, which preserve data integrity, and service interfaces, which hide business logic details from service requestors such as controllers, web services, and other modules.
Web APIs can be bound to service contracts via configuration files.

<a href="#settlement"></a>
### settlement
Settlement occurs when the acquiring bank and the issuer exchange funds and the proceeds are deposited into the merchant account.

<a href="#Shared Catalog"></a>
### Shared Catalog
A feature that allows merchants to create a catalog that can serve as their entire catalog or a subset of it, and then assign custom prices for one or more products.
Merchants can then assign this catalog to one or more companies.
For example, a B2B merchant has three customers who have negotiated specific rates for the merchant’s electronics distribution site.
Using the shared catalog feature, the merchant has:

<a href="#shipment"></a>
### shipment
A shipment contains products to be delivered and generates a record of the products in an order that have been shipped.
More than one shipment can be associated with a single order.

<a href="#shipment document"></a>
### shipment document
A document that accompanies a shipment. The document lists the products and their quantities in the delivery package.

<a href="#shipping carrier"></a>
### shipping carrier
A company that transports packages. Common carriers include UPS, FedEx, DHL, and USPS.

<a href="#shopping cart"></a>
### shopping cart
The set of products that a customer has selected to purchase, but has not yet purchased.
Also refers to an area of an ecommerce site where these products can be found to review and checkout.

<a href="#simple product"></a>
### simple product
The most basic product type, a physical item with a single SKU.
Simple products have various pricing and input controls which makes it possible to sell variations of the product.
Simple products can be used in association with grouped, bundle, and configurable products.
A simple product with custom options is sometimes referred to as a composite product.

<a href="#SKU"></a>
### SKU
Abbreviation for Stock Keeping Unit.
A number or code assigned to a product to identify the product, options, price, and manufacturer.

<a href="#splash page"></a>
### splash page
A promotional page with a product or advertisement; normally displayed before the home page.

<a href="#static block"></a>
### static block
A modular unit of content that can be placed by a user in the CMS on a page to display text and images, or execute snippets of code.
Static blocks contain editable content and can act as landing pages for product categories.
Widgets can be added to static blocks to provide additional functionality.

<a href="#static content"></a>
### static content
User-generated content (not generated by code) that does not change frequently.

<a href="#static files"></a>
### static files
The collection of assets, such as CSS, fonts, images, and JavaScript that is used by a theme.

<a href="#store"></a>
### store
The Commerce scope level of “store” is the second level of your website’s hierarchy, which goes as follows: website &gt; store &gt; store view.
Stores can be organized into one or many. Each store, potentially, has its own root category, and all share catalog and customer data.
Each store can have multiple store views, which are typically used to present the storefront in a different locale and language.



<a href="#store view"></a>
### store view
The Commerce scope level of “store view” refers to the third level in the hierarchy of websites, stores and store views.
Store views typically present the storefront in a different locale and language.
To change store views, use the store chooser in the header.

<a href="#storefront"></a>
### storefront
The online store that customers experience when they visit your Commerce site.

<a href="#T"></a>
## T
<a href="#tax rule"></a>
### tax rule
A combination of a product tax class, customer tax class, and tax rate. This rule defines which tax calculation is applied.

<a href="#template"></a>
### template
Short for HTML template or PHTML template.
A PHTML file contains a mixture of HTML markup and PHP code to inject dynamic content into the HTML.
Most blocks have at least one PHTML (template) file that contains the static HTML generated by the block.
In the Admin, email and newsletter templates combine text, images, and variables with HTML markup to produce personalized content that is sent by the system.

<a href="#theme"></a>
### theme
Contains graphics and appearance information.
Customizes the look and feel of the store.
Mage-OS can ship themes in (Composer) packages.
But themes can be placed under app / design, which is not shipped in a package.
Packages are the unit of download for Composer, and — via Commerce Marketplace — Commerce users can download CE or EE as a series of packages, where packages contain modules, themes, or language packs.

<a href="#U"></a>
## U
<a href="#UI component"></a>
### UI component
A tag designed for Mage-OS software to enable simpler and more flexible user interface (UI) rendering.
The goals of the UI component system include the following:
    - Simplifying Layout Handle XML file
    - Moving Admin user interface elements from HTML+JavaScript to a “pure JavaScript” custom widget system
    - Enabling the creation of more complex UI components out of smaller component
    - Pre-rendering data for UI components as JSON, binding closely to backend data object
    - Using AJAX to update component data
    - Introducing a new DSL for creating the above item

<a href="#UPWARD"></a>
### UPWARD
UPWARD in development.
UPWARD is an acronym for Unified Progressive Web App Response Definition.
An UPWARD definition file describes how a web server delivers and supports a Progressive Web Application.
UPWARD definition files provide details about server behavior using platform-independent, declarative language.
This allows a Progressive Web Application to run on top of an UPWARD-compliant server in any language on any tech stack because the application is only concerned about the HTTP endpoint behavior from the UPWARD server.
An UPWARD server uses a definition file to determine the appropriate process or service for a request from an application shell.
It describes how the server should handle a request and build the response for it.
A PWA project can include an UPWARD definition file to specify its service dependencies.

<a href="#V"></a>
## V
<a href="#Vendor Bundled Extension"></a>
### Vendor Bundled Extension
Vendor-produced code that extends or customizes Commerce behavior and operates as a third-party extension is considered a Vendor Bundled Extension (VBE).
VBEs are thoroughly tested and included with each supported version of Mage-OS Open Source and Mage-OS.
A VBE can include modules, themes, and language packs.

<a href="#vertical scaling"></a>
### vertical scaling
Vertical scaling (scaling up) refers to increasing the processing power of a single server or cluster by adding disk or network I/O, CPUs, or RAM.

<a href="#virtual product"></a>
### virtual product
Represents a non-physical product that can be sold, such as a membership, service, warranty, or subscription.
Virtual products can be sold individually, or included as part of the following product types: grouped product and bundle product.
Does not require shipping or inventory.
The process of creating a virtual product and a simple product is nearly the same.
However, because a virtual product is not shipped, there is no Weight field or option to include a gift card.

<a href="#virtual type"></a>
### virtual type
Virtual types are a way to inject different dependencies into existing PHP classes without affecting other classes and without having to create a class file.
Virtual types can only be referenced by argument overrides in a element within di.xml files, never in source code.
They can’t be extended and they can’t be references as dependencies in a classes constructor.

<a href="#W"></a>
## W
<a href="#website"></a>
### website
In the Mage-OS software, the highest level of a website hierarchy, above store and store view.
You can have multiple websites, and each website can have a different domain name.
Websites can be set up to share customer data, or to not share data.

<a href="#widget"></a>
### widget
A widget is a prepared snippet of code that can be used to place blocks, links, and dynamic content at specific locations on store pages.
You can use widgets to create landing pages for marketing campaigns, display promotional content at specific locations throughout the store.
Widgets can also be used to add interactive elements and action blocks for external review systems, video chats, voting, and subscription forms, or to provide navigation elements for tag clouds and image sliders.