# What's BigTable?

BigTable is a sparsely populated table, which is ideal to store large amount of single-keyed data with low latency.

### Storage Model

BigTable stores data in massively scalable table, each of which is sorted key-value map. The table is composed of rows,
each of which typically describes a single entity, and columns, which contain individual values for each row. A single
value in each row is indexed. This value is known as the row key. Columns that are related to one another are typically
grouped into a column family. Each column is identified by a combination of the column family and a column qualifier,
which is a unique name within the column family.

Each intersection of a row and column can contain multiple cells. Each cell contains a unique timestamped version of the
data for that row and column. Storing multiple cells in a column provides a record of how the stored data for that row
and column has changed over time. BigTable tables are sparse; if a column is not used in a particular row, it does not
take up any space.

Each node in the cluster handles a subset of the requests to the cluster. By adding nodes to a cluster, you can increase
the number of simultaneous requests that the cluster can handle. Adding nodes also increases the maximum throughput for
the cluster. If you enable replication by adding additional clusters, you can also send different types of traffic to
different clusters. Then if one cluster becomes unavailable, you can fail over to another cluster.

**A BigTable table is sharded into blocks of contiguous rows, called tablets, to help balance the workload of queries**.
Tablets are stored on Colossus, a Google-developed file system, in SSTable format. An SSTable provides a persistent,
ordered immutable map from keys to values, where both keys and values are arbitrary byte strings. _Each tablet is
associated with a specific BigTable node_. In addition to the SSTable files, all writes are stored in Colossus's shared
log as soon as they are acknowledged by BigTable, providing increased durability.

Importantly, data is never stored in Bigtable nodes themselves; each node has pointers to a set of tablets that are
stored on Colossus. As a result:

* Rebalancing tablets from one node to another happens quickly, because the actual data is not copied. Bigtable updates
  the pointers for each node.
* Recovery from the failure of a Bigtable node is fast, because only metadata must be migrated to the replacement node.
* When a Bigtable node fails, no data is lost.

### Load Balancing

Each Bigtable zone is managed by a primary process, which balances workload and data volume within clusters. This
process splits busier or larger tablets in half and merges less-accessed/smaller tablets together, redistributing them
between nodes as needed. If a certain tablet gets a spike of traffic, Bigtable splits the tablet in two, then moves one
of the new tablets to another node. Bigtable manages the splitting, merging, and rebalancing automatically, saving you
the effort of manually administering your tablets.

At the same time, it's useful to group related rows so they are next to one another, which makes it much more efficient
to read several rows at the same time.

### Compute

Bigtable provides different compute options depending on your workload requirements. By default, Bigtable uses cluster
nodes for both storage and compute.

## Instance, Cluster & Nodes

Instance in Bigtable are the containers of the data, Instances have one or more clusters located in different zones.
Each cluster has at least 1 node. A table belongs to an instance, not to a cluster or a node.

An instance has a few important properties that you need to know about:

* The edition (Enterprise or Enterprise Plus)
* The storage type (SSD or HDD)
* The application profiles, which are primarily for instances that use replication

A cluster represents the Bigtable service in a specific location. Bigtable instances that have only 1 cluster don't use
replication. If you add a second cluster to an instance, Bigtable automatically starts replicating your data by keeping
separate copies of the data in each of the clusters' zones and synchronizing updates between the copies.

Each cluster in an instance has 1 or more nodes, which are compute resources that Bigtable uses to manage your data.
Behind the scenes, Bigtable splits all of the data in a table into separate tablets. Tablets are stored on disk,
separate from the nodes but in the same zone as the nodes. A tablet is associated with a single node.

Each node is responsible for:

* Keeping track of specific tablets on disk.
* Handling incoming reads and writes for its tablets.
* Performing maintenance tasks on its tablets, such as periodic compactions.



