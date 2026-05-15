# Overview

In Bigtable, a schema is a blueprint or model of a table, including the structure of the following table components:

* Row keys
* Column families, including their garbage collection policies
* Columns

In Bigtable, schema design is driven primarily by the queries, or read requests, that you plan to send to the table.
Because reading a row range is the fastest way to read your Bigtable data, the recommendations on this page are designed
to help you optimize for row range reads. In most cases, that means sending a query based on row key prefixes.

The following general concepts apply to Bigtable schema design:

* Bigtable is a key/value store, not a relational store. It does not support joins, and transactions are supported only
  within a single row.
* Each table has an index: the row key. Each row key must be unique. To create a secondary index, use a continuous
  materialized view. For more information, see Create an asynchronous secondary index.
* Row keys sort rows lexicographically from the lowest to the highest byte string. This order is big-endian (sometimes
  called network byte order), the binary equivalent of alphabetical order.
* Column families are not stored in any specific order.
* Columns are grouped by column family and sorted in lexicographic order within the column family.
* The intersection of a row and column can contain multiple timestamped cells. Each cell contains a unique, timestamped
  version of the data for that row and column.
* Aggregate column families contain aggregate cells. You can create column families that contain only aggregate cells.
  An aggregate lets you merge new data with data already in the cell.
* All operations are atomic at the row level. An operation affects either an entire row or none of the row.
* Ideally, both reads and writes should be distributed evenly across the row space of a table.
* Bigtable tables are sparse. A column doesn't take up any space in a row that doesn't use the column.

> Because all tables in an instance are stored on the same tablets, a schema design that results in hotspots in one
> table can affect the latency of other tables in the same instance. Hotspots are caused by frequently accessing one part
> of the table in a short period of time.

## Tables

Store datasets with similar schemas in the same table, rather than in separate tables.
