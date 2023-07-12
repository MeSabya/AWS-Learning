## What is the access pattern in DynamoDB

An access pattern in DynamoDB refers to the way in which data is accessed in a table. The access pattern determines the read and write throughput for a table and affects the performance and capacity of a table.

**There are two main access patterns in DynamoDB:**

- Key-value access pattern: This is the most common access pattern in DynamoDB and is used to retrieve a single item from a table based on its primary key. This pattern is useful for simple lookups and reads of a single item. It is also known as "Single-Item Actions."

- Query and scan access pattern: This access pattern retrieves multiple items from a table based on the value of one or more non-primary key attributes. The Query operation retrieves items based on a primary key and an optional sort key. The Scan operation retrieves all items in a table or a secondary index. These operations are useful for more complex queries and scans of multiple items.

The key-value access pattern is optimized for read-and-write operations on a single item. In contrast, the query and scan access pattern is optimized for read-and-write operations on multiple items. Choosing the right access pattern for your table depends on your use case and how you plan to access the data in your table.
