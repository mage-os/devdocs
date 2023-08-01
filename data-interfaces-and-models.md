# Data Interfaces and Models Documentation

[TOC]

## Introduction

Data interfaces and models are essential components in Magento 2 development. They provide a structured way to represent
and manipulate data, ensuring consistency and maintainability in your codebase. This documentation will explore the
concepts of data interfaces and models in Magento 2, their purpose, and how to use them effectively.

## Data Interfaces

Data interfaces define the structure and behavior of data objects in Magento 2. They act as contracts that enforce a set
of methods that must be implemented by any class that wants to use or manipulate the data.

Data interfaces are typically defined in the `Api/Data` directory of a module and follow a naming convention
of `EntityInterface`. For example, if you have a module called `Vendor_Module`, the data interface for a custom entity
could be defined in `Vendor/Module/Api/Data/CustomEntityInterface.php`.

Let's take a look at an example data interface for a `CustomEntity`:

```php
<?php

namespace Vendor\Module\Api\Data;

interface CustomEntityInterface
{
    /**
     * Get the entity ID.
     *
     * @return int|null
     */
    public function getId();

    /**
     * Set the entity ID.
     *
     * @param int $id
     * @return $this
     */
    public function setId($id);

    // Other methods...
}
```

In this example, the `CustomEntityInterface` defines two methods: `getId()` and `setId()`. These methods define the
getter and setter for the `id` field of the custom entity.

Data interfaces also define constants that represent the field names. For example, you could define a
constant `FIRST_NAME` to represent the first name field of a customer entity.

By using data interfaces, you can ensure that any class that interacts with the custom entity adheres to a consistent
contract, making your code more maintainable and testable.

## Models

Models in Magento 2 are the implementations of data interfaces. They are responsible for retrieving, manipulating, and
persisting data. Models are typically located in the `Model` directory of a module and follow a naming convention
of `Entity`.

Continuing with our example, let's define a model for the `CustomEntity`:

```php
<?php

namespace Vendor\Module\Model;

use Magento\Framework\Model\AbstractModel;
use Vendor\Module\Api\Data\CustomEntityInterface;

class CustomEntity extends AbstractModel implements CustomEntityInterface
{
    /**
     * Initialize resource model.
     */
    protected function _construct()
    {
        $this->_init(\Vendor\Module\Model\ResourceModel\CustomEntity::class);
    }

    /**
     * Get the entity ID.
     *
     * @return int|null
     */
    public function getId()
    {
        return $this->getData(self::ID);
    }

    /**
     * Set the entity ID.
     *
     * @param int $id
     * @return $this
     */
    public function setId($id)
    {
        return $this->setData(self::ID, $id);
    }

    // Other methods...
}
```

In this example, the `CustomEntity` model extends the `AbstractModel` class provided by Magento 2. This abstract class
provides common functionality for models, such as data storage and retrieval.

The model implements the `CustomEntityInterface`, which enforces the implementation of the methods defined in the
interface. The implementation of the methods simply delegates the calls to the `getData()` and `setData()` methods
provided by the `AbstractModel` class.

Models should also define a constructor that initializes the resource model. The resource model is responsible for
interacting with the database or other data storage mechanisms. In this example, the resource model for `CustomEntity`
is defined in `Vendor/Module/Model/ResourceModel/CustomEntity.php`.

By utilizing models, you can encapsulate the logic for retrieving and manipulating data in a structured and consistent
manner.

## Conclusion

Data interfaces and models play a crucial role in Magento 2 development, providing a structured way to represent and
manipulate data. By defining data interfaces, you can enforce a consistent contract for interacting with data objects.
Models, on the other hand, are responsible for implementing these interfaces, encapsulating the logic for data retrieval
and manipulation.

By following the conventions and best practices outlined in this documentation, you can ensure the maintainability and
consistency of your Magento 2 codebase.
