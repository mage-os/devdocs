# Search Documentation

[TOC]

## Introduction

This documentation provides a comprehensive guide to implementing and optimizing search functionality in a PHP-based
e-commerce platform, specifically Magento 2. It covers the key concepts, techniques, and best practices for search
implementation and customization. By following this guide, you will be able to enhance the search experience for your
users and improve the overall performance of your application.

## 1. Search Basics

Search functionality is a crucial aspect of any e-commerce platform, allowing users to quickly find products or
information they are looking for. In Magento 2, search is primarily based on Elasticsearch, an open-source, distributed
search engine. Elasticsearch provides advanced features like full-text search, relevance ranking, and filtering.

To implement search in Magento 2, you need to have Elasticsearch configured and running. You can check the official
Magento 2 documentation for detailed instructions on Elasticsearch setup.

## 2. Search Types

Magento 2 supports two types of search: Quick Search and Advanced Search.

### Quick Search

Quick Search is the default search functionality in Magento 2. It enables users to perform a keyword-based search across
various attributes of products, like name, description, and SKU. The search query is matched against the indexed data,
and relevant results are displayed.

Here's an example code snippet to perform a Quick Search in Magento 2:

```php
$searchQuery = 'magento';
$searchResults = $objectManager->create('Magento\CatalogSearch\Model\Search')
    ->setQuery($searchQuery)
    ->getSearchResult();
```

### Advanced Search

Advanced Search allows users to perform more complex searches by specifying multiple criteria, such as category, price
range, and attribute values. It provides a more refined search experience and helps users find products based on
specific requirements.

To perform an Advanced Search in Magento 2, you can use the following code snippet:

```php
$advancedSearchModel = $objectManager->create('Magento\CatalogSearch\Model\Advanced');
$advancedSearchModel->addFilters([
    'name' => 'magento',
    'price' => [
        'from' => 10,
        'to' => 100
    ]
]);
$searchResults = $advancedSearchModel->getProductCollection();
```

## 3. Search Indexing

Search indexing is the process of preparing and organizing data for efficient search operations. In Magento 2,
Elasticsearch is responsible for indexing product data and attributes. By default, Magento 2 includes common product
attributes in the search index, like name, description, and SKU. However, you can customize the indexing process and
include additional attributes if needed.

To customize the search index in Magento 2, you can create a custom module and define a `search_request.xml` file. This
file specifies the attributes to be included in the search index. Here's an example `search_request.xml` file:

```xml
<requests xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:noNamespaceSchemaLocation="urn:magento:framework:Search/etc/search_request.xsd">
    <request query="quick_search_container">
        <dimensions>
            <attribute name="name"/>
            <attribute name="description"/>
            <attribute name="sku"/>
            <attribute name="custom_attribute"/>
        </dimensions>
    </request>
</requests>
```

After creating the `search_request.xml` file, you need to run the following command to apply the changes:

```bash
php bin/magento indexer:reindex catalogsearch_fulltext
```

## 4. Search Querying

Querying is the process of retrieving relevant search results based on user input. Elasticsearch provides a powerful
Query DSL (Domain-Specific Language) that allows you to construct complex queries and apply filters, aggregations, and
sorting.

In Magento 2, you can use the `SearchCriteria` class to build search queries. Here's an example code snippet to perform
a search query in Magento 2:

```php
$searchCriteria = $objectManager->create('Magento\Framework\Api\SearchCriteriaBuilder')
    ->addFilter('name', 'magento', 'like')
    ->addSortOrder('price', 'ASC')
    ->setPageSize(10)
    ->create();

$searchResults = $objectManager->create('Magento\Catalog\Api\ProductRepositoryInterface')
    ->getList($searchCriteria);
```

## 5. Search Optimization

Optimizing search functionality is crucial for improving performance and user experience. Here are some best practices
for search optimization in Magento 2:

- Configure Elasticsearch settings for optimal performance, like the number of shards and replicas.
- Use appropriate analyzers to handle different languages and search requirements.
- Optimize attribute mapping to improve relevance and search accuracy.
- Leverage Elasticsearch features like aggregations, highlighting, and suggesters to enhance the search experience.

Ensure to monitor and measure the performance of your search implementation using tools like Elasticsearch's Query
Profiler and Magento 2's built-in logging and reporting features.

## 6. Conclusion

This documentation provided an in-depth understanding of search implementation and customization in Magento 2. You
learned about Quick Search and Advanced Search, search indexing, querying, and optimization techniques. By following
these best practices, you can enhance the search functionality of your PHP-based e-commerce platform and provide a
seamless and efficient search experience to your users.

Happy searching!
