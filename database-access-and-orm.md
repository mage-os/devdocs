# Database Access and ORM Documentation

[TOC]

## Introduction

Database access and Object-Relational Mapping (ORM) are fundamental concepts in software development. In this
documentation, we will explore the various aspects of database access and ORM, specifically in the context of PHP and
Magento 2. We will discuss the importance of these concepts, their benefits, and provide concrete examples and code
snippets to demonstrate their usage.

## Database Access

### Connecting to a Database

To interact with a database in PHP, you need to establish a connection. In Magento 2, this can be achieved using
the `Magento\Framework\App\ResourceConnection` class. Here's an example:

```php
<?php
use Magento\Framework\App\ResourceConnection;

$connection = $objectManager->get(ResourceConnection::class)->getConnection();
```

### Executing Queries

Once you have a connection, you can execute SQL queries. The `Magento\Framework\DB\Adapter\AdapterInterface` interface
provides methods like `query`, `fetchRow`, `fetchAll`, etc., to execute queries and retrieve results. Here's an example:

```php
<?php
use Magento\Framework\DB\Adapter\AdapterInterface;

$select = $connection->select()
    ->from('catalog_product_entity')
    ->where('price > ?', 100);

$result = $connection->fetchAll($select);
```

### Retrieving Data

Fetching data from a database table involves executing a query and processing the results. You can use the `fetchRow`
method to retrieve a single row, or `fetchAll` to get multiple rows as an array. Here's an example:

```php
<?php
use Magento\Framework\DB\Adapter\AdapterInterface;

$productId = 42;

$select = $connection->select()
    ->from('catalog_product_entity')
    ->where('entity_id = ?', $productId);

$product = $connection->fetchRow($select);

echo $product['name'];
```

### Inserting Data

To insert data into a database table, you can use the `insert` method provided by the `AdapterInterface`. Here's an
example:

```php
<?php
use Magento\Framework\DB\Adapter\AdapterInterface;

$data = [
    'name' => 'New Product',
    'price' => 99.99,
];

$connection->insert('catalog_product_entity', $data);
```

### Updating Data

Updating existing data in a database table is done using the `update` method. You specify the table name, the data to
update, and any conditions. Here's an example:

```php
<?php
use Magento\Framework\DB\Adapter\AdapterInterface;

$data = [
    'price' => 109.99,
];

$where = ['entity_id = ?' => 42];

$connection->update('catalog_product_entity', $data, $where);
```

### Deleting Data

To delete data from a database table, you can use the `delete` method. It requires the table name and any conditions to
specify which rows to delete. Here's an example:

```php
<?php
use Magento\Framework\DB\Adapter\AdapterInterface;

$where = ['entity_id = ?' => 42];

$connection->delete('catalog_product_entity', $where);
```

## ORM (Object-Relational Mapping)

### Mapping Database Tables to PHP Classes

ORM allows you to map database tables to PHP classes, making it easier to work with data in an object-oriented manner.
In Magento 2, this is achieved using the Entity-Attribute-Value (EAV) system. Each database table corresponds to an
entity, and each column represents an attribute. Here's an example:

```php
<?php
namespace Vendor\Module\Model;

use Magento\Framework\Model\AbstractModel;

class Product extends AbstractModel
{
    protected function _construct()
    {
        $this->_init('Vendor\Module\Model\ResourceModel\Product');
    }
}
```

### CRUD Operations with ORM

ORM simplifies CRUD (Create, Read, Update, Delete) operations by providing methods to perform these operations on
entities. For example, to create a new entity, you can use the `create` method. Here's an example:

```php
<?php
use Vendor\Module\Model\ProductFactory;

$product = $objectManager->get(ProductFactory::class)->create();
$product->setName('New Product');
$product->setPrice(99.99);
$product->save();
```

### Fetching Related Data

ORM allows you to easily fetch related data using relationships defined in the entity classes. For example, if
a `Product` entity has a many-to-one relationship with a `Category` entity, you can fetch the category of a product
using the `getCategory` method. Here's an example:

```php
<?php
$product = $objectManager->get(ProductFactory::class)->create()->load($productId);
$category = $product->getCategory();
```

### Updating and Saving Entities

Updating an entity is as simple as loading it and modifying its attributes. Once you've made the changes, you can save
the entity back to the database using the `save` method. Here's an example:

```php
<?php
$product = $objectManager->get(ProductFactory::class)->create()->load($productId);
$product->setName('Updated Product');
$product->save();
```

### Deleting Entities

To delete an entity, you can use the `delete` method. Here's an example:

```php
<?php
$product = $objectManager->get(ProductFactory::class)->create()->load($productId);
$product->delete();
```

## Conclusion

In this documentation, we covered the concepts of database access and ORM in PHP and Magento 2. We discussed connecting
to a database, executing queries, retrieving and manipulating data, and using ORM for simplified CRUD operations. By
leveraging these concepts effectively, you can build robust and efficient applications that interact seamlessly with
databases.
