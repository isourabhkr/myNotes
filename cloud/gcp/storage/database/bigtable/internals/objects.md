# Tables

A Bigtable _Table_ is a sorted key-valued map that stores data in row and columns. Each row is indexed by single, unique
row key. Columns that are related to each other are typically grouped into column family.

Bigtable has flexible data model, and the tables are sparse. This means that if a column is unused in a row, no data is
stored for the column.
In a row, a column can contain multiple cells, each identified by the four-tuple (row key, column family, column
qualifier, timestamp). Storing multiple cells in a column provides a record of how the stored data for that row and
column has changed over time.

A Bigtable table doesn't support joins, and transactions are supported only within a single row.

A table is an instance-level resource that is automatically replicated to every cluster in the instance. Data retention
is controlled with garbage collection policies that are set at the column-family level.

To optimize performance, Bigtable continuously splits tables across multiple nodes, evenly distributing the amount of
data stored on each node, and keeping frequently accessed rows spread apart where possible. This ongoing process is
automatic.

## Important nuances

1. While creating a new table providing table split, while creating the table multiple row kys can be provided and
   BigTable will split the table at the row key, and store it into different nodes. Row keys can be beneficial when a
   new large table is getting created and Bigtable don't know about the query patterns to split the load across
   different nodes.
2. Modify column families in a table
3. Set garbage collection policies: A garbage collection policy tells Bigtable which data to keep and which data to mark
   for deletion. Garbage collection policies are set at the column family level. These can be provided while creating
   the table or later. Column family can be managed to have number of cells each column in the family must have. If not
   provided it takes default behaviour which depends on the way the table was created.

# Views

There are below types of views in BigTable.

1. Logical View: A logical view – often referred to as just a view – is the result of a SQL query. It functions as a
   virtual table that can be queried by other SQL queries

2. Continuous materialized views: A continuous materialized view is created by continuously running a SQL query against
   a Bigtable table. Bigtable creates a new table based on the query output and keeps it in sync with the source
   table. These Type of views are read only. In a nutshell it creates a new table with a different schema. Hence, the
   costs are also associated with storage of a continuous materialized view as well as for the processing work that goes
   into creating the second table, keeping it in sync with the source table, and replicating it.
3. Authorized views: Authorized views are views of tables that you configure to include specific table data and then
   grant access to separately from access to the source table. It's a subset of the

### Continuous materialized views

In Bigtable, a continuous materialized view is the result of a continuous, fully-managed background process. This
process uses the sql query to create and maintain a precomputed table that Bigtable updates incrementally as the source
data changes.

Data in a continuous materialized view includes the following:

* Aggregated or transformed values that are derived from data in the source table
* Unaggregated values that define the grouping key





---
Reference

1. https://docs.cloud.google.com/bigtable/docs/managing-tables#gcloud 
