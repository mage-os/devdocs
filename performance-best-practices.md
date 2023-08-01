# Performance Best Practices

[TOC]

This document aims to provide a comprehensive guide on performance best practices for PHP and Magento 2. By following
these recommendations, you can optimize the performance of your PHP code and improve the overall speed and efficiency of
your Magento 2 application. The guidelines discussed here are based on industry best practices and can help you achieve
faster page load times, reduce server load, and enhance the overall user experience.

## Caching

Caching is an essential technique for improving performance in PHP and Magento 2 applications. By caching frequently
accessed data, you can avoid the need to generate the same content repeatedly, reducing the load on your server and
improving response times. There are several caching mechanisms available in Magento 2:

### Full Page Caching

Magento 2 provides built-in full page caching, which can significantly improve the performance of your store. You can
enable full page caching from the Magento Admin panel under **Stores > Configuration > Advanced > System > Full Page
Cache**. This feature caches complete HTML pages, bypassing expensive database queries and PHP rendering for subsequent
requests.

### Object Caching

Magento 2 supports various object caching mechanisms, such as Redis and Memcached, which can be configured from the
Magento Admin panel. These caching systems store PHP objects in memory, allowing for faster retrieval, eliminating the
need to recompute expensive calculations or database queries.

Here's an example code snippet to enable Redis caching in Magento 2:

```php
<?php
return [
    'backend' => [
        'frontName' => 'admin'
    ],
    'cache' => [
        'frontend' => [
            'default' => [
                'backend' => 'Cm_Cache_Backend_Redis',
                'backend_options' => [
                    'server' => 'redis.example.com',
                    'port' => '6379'
                ]
            ],
            'page_cache' => [
                'backend' => 'Cm_Cache_Backend_Redis',
                'backend_options' => [
                    'server' => 'redis.example.com',
                    'port' => '6379'
                ]
            ]
        ]
    ]
];
```

## Database Optimization

Efficient database queries are fundamental for good performance. Here are some techniques to optimize your database
operations:

### Indexing

Ensure that your database tables are properly indexed. Indexes can significantly speed up data retrieval operations by
allowing the database engine to quickly locate the required data. Analyze your most frequently executed queries and
identify the columns involved in WHERE or ORDER BY clauses. Then, add indexes on those columns to improve query
performance.

```sql
CREATE INDEX idx_customer_email ON customer_entity (email);
```

### Query Optimization

Review your SQL queries and optimize them for execution speed. Consider techniques like joining tables instead of using
subqueries, avoiding unnecessary SELECT * statements, and using appropriate WHERE and ORDER BY clauses.

Example of a poorly optimized query:

```sql
SELECT *
FROM sales_order
WHERE customer_id IN (SELECT customer_id FROM customer_entity WHERE is_active = 1);
```

Optimized version of the above query using JOIN:

```sql
SELECT so.*
FROM sales_order AS so
         INNER JOIN customer_entity AS ce ON so.customer_id = ce.customer_id
WHERE ce.is_active = 1;
```

## Code Optimization

Efficient code is essential for achieving optimal performance. Here are some code optimization techniques for PHP and
Magento 2:

### Minify CSS and JavaScript

Minifying your CSS and JavaScript files reduces their file size, resulting in faster download times for your users.
Tools like [CSSMin](https://github.com/tubalmartin/YUI-CSS-compressor-PHP-port)
and [JSMin](https://github.com/mrclay/minify) can help you automatically minify your static assets during the deployment
process.

### Use Composer Autoloader

Make sure to utilize the Composer autoloader for efficient class loading. Composer autoloads classes on-demand, reducing
the overhead of loading unnecessary classes. Ensure that the Composer autoloader is configured and optimized in your
project.

```php
<?php
require_once 'vendor/autoload.php';
```

### Optimize Database Queries

When executing database queries, use optimized techniques like prepared statements. Prepared statements not only prevent
SQL injection vulnerabilities but also improve performance by allowing the database engine to reuse query execution
plans.

Example of an insecure query:

```php
<?php
$sql = "SELECT * FROM customers WHERE email = '" . $_GET['email'] . "'";
```

Secure and optimized version using prepared statements:

```php
<?php
$email = $_GET['email'];
$stmt = $pdo->prepare("SELECT * FROM customers WHERE email = ?");
$stmt->execute([$email]);
```

## Caching in Custom Modules

If you are developing custom modules for Magento 2, make sure to utilize the caching mechanisms provided by the
framework. Utilizing built-in caching can significantly improve the performance of your custom code. You can leverage
the Magento cache types to store the results of expensive operations or frequently accessed data.

For example, let's assume you have a custom module that fetches a list of products. Instead of querying the database on
every request, you can cache the product data and retrieve it from the cache for subsequent requests.

```php
<?php
use Magento\Framework\App\CacheInterface;

class ProductList
{
    private $cache;
    
    public function __construct(CacheInterface $cache)
    {
        $this->cache = $cache;
    }
    
    public function getProductList()
    {
        $cacheKey = 'product_list';
        $productList = $this->cache->load($cacheKey);
        
        if (!$productList) {
            // Expensive database query to fetch product list here
            $productList = $this->fetchProductListFromDatabase();
            
            // Store the product list in cache
            $this->cache->save($productList, $cacheKey, ['product_list'], 3600);
        }
        
        return $productList;
    }
}
```

## Conclusion

By following the performance best practices outlined in this document, you can optimize the speed and efficiency of your
PHP and Magento 2 applications. Remember to utilize caching mechanisms, optimize your database queries, and write
efficient code. Regularly monitor and analyze your application's performance to identify bottlenecks and further
optimize your codebase.
