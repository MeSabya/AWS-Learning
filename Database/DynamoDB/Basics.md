# Defination

```Lua
Amazon DynamoDB is a key-value and document database, which delivers single-digit millisecond performance at any scale. 
It’s a fully managed, multi-region, multi-active, durable database with built-in security, backup and restoration, 
and in-memory caching for internet-scale applications.
```
👉 DynamoDB is a simple database that supports key-value and document-based table design.

## Salient Features of DynamoDB

- Fully managed:
  It is a fully-managed database. That means you do not need to worry about the servers and software updates. You just have to worry about using and managing your data.
- Fast: it does give single-digit millisecond latency at very high scales.  

- Durable and highly available#
  DynamoDB replicates our data to provide total durability.DynamoDB gives “always available” writes. 
  We can always write to your data without any delay.
  For reads, DynamoDB provides high availability with eventual consistency. 
  The consistency is not a big tradeoff for most of the applications. Additionally, DynamoDB is fast and the data becomes consistent within a few milliseconds.
- Flexible/schema-less:
  The only schema constraint you have when inserting an item in a table is that the item should have a unique primary key. 
  As long as we provide a unique primary key, we can insert whatever data we want to insert


## Core Components of Amazon DynamoDB

**Tables, Items, and Attributes**

The following are the basic DynamoDB components:

### Tables – 

Similar to other database systems, DynamoDB stores data in tables. A table is a collection of data. For example, see the example table called People that you could use to store personal contact information about friends, family, or anyone else of interest. You could also have a Cars table to store information about vehicles that people drive.

### Items – 

Each table contains zero or more items. An item is a group of attributes that is uniquely identifiable among all of the other items. In a People table, each item represents a person. For a Cars table, each item represents one vehicle. Items in DynamoDB are similar in many ways to rows, records, or tuples in other database systems. In DynamoDB, there is no limit to the number of items you can store in a table.

### Attributes – 

Each item is composed of one or more attributes. An attribute is a fundamental data element, something that does not need to be broken down any further. For example, an item in a People table contains attributes called PersonID, LastName, FirstName, and so on. For a Department table, an item might have attributes such as DepartmentID, Name, Manager, and so on. Attributes in DynamoDB are similar in many ways to fields or columns in other database systems.

### Primary Key -

The primary key uniquely identifies each item in the table, so that no two items can have the same key.

DynamoDB supports two different kinds of primary keys:

**Partition key** – 

A simple primary key, composed of one attribute known as the partition key.

DynamoDB uses the partition key's value as input to an internal hash function. The output from the hash function determines the partition (physical storage internal to DynamoDB) in which the item will be stored.

In a table that has only a partition key, no two items can have the same partition key value.

The People table described in Tables, Items, and Attributes is an example of a table with a simple primary key (PersonID). You can access any item in the People table directly by providing the PersonId value for that item.

![image](https://user-images.githubusercontent.com/33947539/154117228-47c9d4c9-698e-4f4b-804b-ecf07de4bd69.png)

**Partition key and sort key** -

DynamoDB uses the partition key value as input to an internal hash function. The output from the hash function determines the partition (physical storage internal to DynamoDB) in which the item will be stored. All items with the same partition key value are stored together, in sorted order by sort key value.

In a table that has a partition key and a sort key, it's possible for multiple items to have the same partition key value. However, those items must have different sort key values.

![image](https://user-images.githubusercontent.com/33947539/154120250-b1969bd1-7a7c-4822-98e2-1f8b7d690268.png)

### Secondary Indexes
AWS DynamoDB being a No SQL database doesn’t support queries such as SELECT with a condition such as the following query.
          SELECT * FROM Users
          WHERE email='username@email.com';

Note that when doing the query above with an SQL database, a query optimizer evaluates available indexes to see if any index can fulfill the query.

It is possible to obtain the same query result using DynamoDB scan operation. However, scan operations access every item in a table which is slower than query operations that access items at specific indices. Imagine, you have to look for a book in a library by going through possibly all the books in the library versus you know which shelf the book is at.
Thus, there is a need for another table or data structure that stores data with different primary key and maps a subset of attributes from this base table. 
This other table is called a **secondary index** and is managed by AWS DynamoDB. When items are added, modified, or deleted in the base table, associated secondary indexes will be updated to reflect the changes.

**AWS DynamoDB supports two types of indexes: Global Secondary Index (GSI) and Local Secondary Index (LSI).**

Global secondary index is an index that have a partition key and an optional sort key that are different from base table's primary key. It is deemed "global" because queries on the index can access the data across different partitions of the base table. It can viewed as a different table that contains attributes based on the base table.

Local secondary index is an index that must have the same partition key but a different sort key from the base table. It is considered "local" because every partition of a local secondary index is bounded by the same partition key value of the base table. It enables data query with different sorting order of the specified sort key attribute.

![image](https://user-images.githubusercontent.com/33947539/154124431-7d763379-c99b-4a66-b711-109f7f514ef1.png)

#### GSI Example
Consider this table that contains Uuid as primary key, UserId and Data attributes.

                | Uuid(Partition Key) | UserId | Data |

With this base table key schema, it can answer queries to retrieve data for a uuid. However, to get all data for a user id, it would have to do a scan query and get all the items that have matching user id.
To be able to get all data for a user efficiently, you can use a global secondary index that has UserId as its primary key (partition key). Using this index, you can do a query to retrieve all data for a user.

#### LSI Example

Consider the table below:

        |UserId(Partition Key) | ArticleName(Sort Key) | DateCreated | Data| 

With this base table key schema, it can answer queries to retrieve all the article sorted by names for a specific user(query by UserId). However, to retrieve all the articles associated with a user sorted by date created, you would have to retrieve all the articles first and sort them.
With a local secondary index that has UserId as its partition key and DateCreated as its sort key, you can retrieve a user’s articles sorted by date created.

       |UserId(Partition Key) | DateCreated(Sort Key) | ArticleName | Data|
       
       
## Summary 

![image](https://user-images.githubusercontent.com/33947539/155927591-9a94853a-8cd0-4534-9b18-bcd355708f77.png)

- Every DynamoDB Table is divided in to one or more Partitions.
- Each Partition contains a subset of the table data, in addition to any Local Secondary Indexes* created on that Partition data
- Global Secondary Indexes are stored and maintained separately from the Partitions and they index the entire table (not specific to any one Partition)

*DynamoDB internals are not visible to public. So, the internal partition structure shown above is only an illustration intended to explain the observed behaviour*

![image](https://user-images.githubusercontent.com/33947539/155927659-0a9f0091-b24e-4d42-af46-2f848e54442e.png)

**As per the above image:**

- Each Table consists of a number of Items
- Each Item can contain one or more Attributes
- Every Item must contain at least one Attribute, which will be its Partition Key
- For every CRUD operation on the table, the operation must specify the Item’s Partition Key
- In addition to the Partition Key, a Table definition can assign any Attribute as its Sort Key
- Read operations on the Table can specify Sort Key, for more advanced queries (“contains”, “begins with” etc.,)
- A group of Items in table is called an Item Collection





