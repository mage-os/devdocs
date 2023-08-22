# Indexer.xml File Reference Documentation

The indexer.xml file is an important configuration file in Magento 2 that defines the behavior of indexers. Indexers are
responsible for updating and retrieving data from the database to improve the performance of query execution.

## File Location

The indexer.xml file is located in the `etc` directory of your custom module or theme. The file path is as follows:

```
app/code/[Vendor]/[Module]/etc/indexer.xml
```

Alternatively, for a theme, the file path is:

```
app/design/frontend/[Vendor]/[Theme]/etc/indexer.xml
```

## File Structure

The indexer.xml file follows a specific structure that defines how indexers are configured. It consists of three main
sections:

1. `<config>` - This is the root element that encloses all the other sections of the indexer.xml file.
2. `<indexer>` - This section defines the individual indexers and their configuration.
3. `<data>` - This section specifies the sources of data that indexers will use to update or retrieve data from the
   database.

Here is an example of the basic structure of the indexer.xml file:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Indexer/etc/indexer.xsd">
    <indexer id="[Indexer_ID]" view_id="[Indexer_View_ID]">
        <!-- Indexer configuration goes here -->
        <data_source name="[Data_Source_Name]">
            <!-- Data source configuration goes here -->
        </data_source>
    </indexer>
</config>
```

## Defining Indexers

To define an indexer, you need to add a `<indexer>` section within the `<config>` section of the indexer.xml file.
Each `<indexer>` section should have a unique `id` attribute and a `view_id` attribute that identifies the indexer's
view.

Here is an example of a custom indexer definition:

```xml
<indexer id="my_custom_indexer" view_id="my_custom_indexer">
    <!-- Indexer configuration goes here -->
</indexer>
```

## Configuring Indexers

Within the `<indexer>` section, you can define various aspects of the indexer's behavior. Some of the key configuration
options include:

- `<title>` - Specifies the title of the indexer that will be displayed in the Magento admin panel.
- `<description>` - Provides a brief description of the indexer's purpose.
- `<model>` - Specifies the class responsible for performing the indexing operations.
- `<indexer_id>` - Specifies the unique identifier for the indexer.
- `<status>` - Sets the initial status of the indexer (e.g., `Working`, `Scheduled`, `Invalid`, etc.).
- `<depends>` - Specifies any dependencies that the indexer has on other indexers.

Here is an example of a custom indexer configuration:

```xml
<indexer id="my_custom_indexer" view_id="my_custom_indexer">
    <title>My Custom Indexer</title>
    <description>This indexer updates the custom data in the database.</description>
    <model>[Vendor]\[Module]\Model\Indexer\MyCustomIndexer</model>
    <indexer_id>my_custom_indexer</indexer_id>
    <status>Working</status>
    <depends>
        <indexer>[Other_Module]::indexer_id</indexer>
    </depends>
</indexer>
```

## Configuring Data Sources

Data sources are the entities from which the indexers retrieve or update data. Each `<indexer>` section can have one or
more `<data_source>` sections to specify the sources of data.

Here is an example of a data source configuration:

```xml
<data_source name="[Data_Source_Name]">
    <!-- Data source configuration goes here -->
</data_source>
```

The `[Data_Source_Name]` should match the name specified in the `<data_source>` section of the indexer.xml file.

## Conclusion

The indexer.xml file is an essential configuration file in Magento 2 that defines the behavior of indexers. By
understanding its structure and the available configuration options, you can effectively configure and manage indexers
in your custom modules or themes.
