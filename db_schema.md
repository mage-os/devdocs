# DB_SCHEMA.XML Reference Documentation

## Introduction

The `db_schema.xml` file is an essential part of the Magento 2 module development process. It provides a way to define
the database schema for your module, including tables, columns, indexes, and other related entities. This reference
documentation aims to explain the various elements and attributes used in the `db_schema.xml` file and provide concrete
examples and code snippets for better understanding.

## File Structure

The `db_schema.xml` file should be located in the `etc` directory of your module. It follows a specific XML structure,
as follows:

```xml
<?xml version="1.0"?>
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <!-- Define your tables, columns, indexes, and other entities here -->
</schema>
```

In the above code snippet, you can see the XML declaration at the beginning and the root `schema` element, which serves
as the container for defining your module's database schema.

## Tables

To define a table in your module's schema, you should use the `table` element within the `schema` element. The `table`
element can have the following attributes:

- `name`: The name of the table.
- `resource`: The resource name used to retrieve a database connection.
- `engine`: The storage engine used for the table (optional, defaults to `innodb`).

Here's an example of defining a table in the `db_schema.xml` file:

```xml
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="my_module_table" resource="default" engine="innodb">
        <!-- Define your columns, indexes, and other entities here -->
    </table>
</schema>
```

## Columns

Within a table, you can define columns using the `column` element. The `column` element can have the following
attributes:

- `name`: The name of the column.
- `dataType`: The data type of the column.
- `length`: The length of the column (optional, depends on the data type).
- `nullable`: Whether the column allows NULL values (`true` or `false`, optional, defaults to `false`).
- `comment`: A descriptive comment for the column (optional).

Here's an example of defining columns within a table:

```xml
<table name="my_module_table" resource="default" engine="innodb">
    <column name="id" dataType="int" nullable="false" comment="ID"/>
    <column name="name" dataType="varchar" length="255" nullable="true"/>
    <!-- Define more columns here -->
</table>
```

## Indexes

You can define indexes for a table using the `index` element within the `table` element. The `index` element can have
the following attributes:

- `name`: The name of the index.
- `indexType`: The type of the index (`btree`, `fulltext`, or `hash`, optional, defaults to `btree`).
- `referenceId`: The name of the column being referenced by the index.
- `referenceTable`: The name of the table being referenced by the index.

Here's an example of defining an index within a table:

```xml
<table name="my_module_table" resource="default" engine="innodb">
    <column name="id" dataType="int" nullable="false" comment="ID"/>
    <column name="name" dataType="varchar" length="255" nullable="true"/>

    <index name="IDX_MY_MODULE_TABLE_ID" indexType="btree">
        <column name="id"/>
    </index>
</table>
```

## Foreign Keys

To define a foreign key constraint between two tables, you can use the `constraint` element within the `table` element.
The `constraint` element can have the following attributes:

- `name`: The name of the foreign key constraint.
- `referenceId`: The name of the column being referenced by the foreign key.
- `referenceTable`: The name of the table being referenced by the foreign key.
- `onDelete`: The action to perform when the referenced row is deleted (`cascade`, `set null`, `set default`,
  or `restrict`, optional, defaults to `restrict`).
- `onUpdate`: The action to perform when the referenced row is updated (`cascade`, `set null`, `set default`,
  or `restrict`, optional, defaults to `restrict`).

Here's an example of defining a foreign key constraint within a table:

```xml
<table name="my_module_table" resource="default" engine="innodb">
    <column name="id" dataType="int" nullable="false" comment="ID"/>
    <column name="name" dataType="varchar" length="255" nullable="true"/>

    <constraint xsi:type="foreign" referenceId="id" referenceTable="another_module_table" onDelete="cascade"
                onUpdate="restrict"/>
</table>
```

## Conclusion

The `db_schema.xml` file provides a way to define the database schema for your Magento 2 module. By understanding its
elements and attributes, you can effectively define tables, columns, indexes, and foreign keys. This reference
documentation aimed to provide a comprehensive overview of the `db_schema.xml` file and its usage in Magento 2 module
development.
