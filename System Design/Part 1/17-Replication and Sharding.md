# Replication and Sharding

Replication and sharding are two techniques commonly used together in a distributed system to achieve high availability and throughput. Let's explore them in detail.

## Replication

When a single database cannot handle all incoming requests, replication comes into play. Replication involves creating a copy of the database called a replica. The replica(s) is hosted on a separate machine or server, and it is kept in sync with the original database. Replication is used to increase data availability, improve scalability, and increase data durability.

The original database is the _leader_ or _master_, while the replica is the _follower_ or _slave_.

In a leader/follower architecture, data replication flows from the leader to the follower, and the leader is responsible for updating the follower. If replication were attempted from the follower to the leader, the leader would not be fully updated.

There are two ways in which replication occurs: asynchronously and synchronously.

### Synchronous Replication

In synchronous replication, every write transaction on the leader is immediately replicated on the follower, ensuring consistency between the two replicas. However, this approach introduces latency. The benefit is that if the leader goes down, the mostly updated follower can take its place, providing high availability.

![sync-replication](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/32c9a48c-9b08-4e10-9111-53780a437e00/sharpen=1)

> The visual above demonstrates how synchronous replication works. So while it is synchronous and the data will be consistent, client 1 will only get feedback once the leader has finished replication.

### Asynchronous Replication

Asynchronous replication involves a delay in data replication. The leader database commits the transaction and sends replication data to the follower without waiting for the follower to acknowledge or apply the changes immediately. This reduces latency, but it means that if a client makes a request to the follower before the leader has updated it, the data might be stale until the leader updates it. This is the trade-off made for increased availability.

![async-replication](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/2c574641-80e8-491e-38db-0b3b2a898c00/sharpen=1)

> The visual above demonstrates async replication. Because data is being replicated async, client 2 might get stale data upon request.

### Master-Master (Multi-Master) Replication

Master-Master replication is used when data needs to be served in different regions. For example, one leader might serve the west while another serves the east. Both leaders can be written to and read from, making it ideal for distributing data across different parts of the world. However, synchronization latency between the leaders can be a challenge, and measures like periodic updates are needed to keep them in sync.

![async-replication](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/ec88dd6e-3a50-47d0-73e3-cb6d23f2bc00/sharpen=1)

## Sharding

Sharding is used when replication alone is insufficient to handle the high traffic volume on a single database. It involves dividing the database into smaller shards, each hosted on a separate machine or server. By distributing data and workload across multiple shards, the system achieves improved performance, scalability, and availability. Each shard contains only a subset of the entire dataset, and they do not have a complete copy of the original database.

Now, because we have multiple shards, what decides how data gets partitioned?

One approach is the range-based approach. Under this approach, data is split according to ranges. If we apply this to our 100 row approach with our four shards, we might split it by having `1-25`, `26-50`, `51-75` and `76-100`, where these numbers are the IDs.

Determining how data is partitioned among shards is done using a shard key. The shard key is a chosen criterion or attribute that determines which shard each data belongs to. For example, in a relational database, the shard key might be based on sex, such as splitting data between male and female. Alternatively, it could be based on a first name/last name basis, such as dividing names from A-L and M-Z into separate shards.

![async-replication](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/c8b9f646-1625-447a-532f-acd377548400/sharpen=1)

> The visual above demonstrates a database table being sharded, where the shard key is s_name.

## Challenges with sharding

While sharding is effective for handling high traffic, it comes with its own challenges. For instance, when dealing with hundreds of tables, ensuring related tables with related data end up in the same shard can be complex. Additionally, maintaining the ACID (Atomicity, Consistency, Isolation, Durability) properties poses challenges in sharding relational databases, as they are not designed for distribution. SQL databases like MySQL and PostgreSQL do not inherently support sharding, requiring developers to implement sharding logic at the application level, which can become complicated.

On the other hand, NoSQL databases, designed with horizontal scaling in mind, are better suited for sharding, as they do not have the same constraints as relational databases. They offer eventual consistency, where data consistency across nodes is achieved over time.

Because our data is non-relational in NoSQL databases, we don't have the same constraints that we have when we are using relational databases. NoSQL databases were designed with horizontal scaling in mind so these limitations don't apply as much to non-relational databases. The data does not even need to be consistent from the nodes - it just needs to be eventually consistent.

> Eventual consistency refers to the property of a distributed system, particularly in NoSQL databases, where replicas of data will eventually become consistent with each other over time. It means that after a write operation, different replicas may temporarily have different versions of the data, but they will eventually converge to a consistent state.

> We can also use hash based sharding and this is a good use case for consistent hashing, which we learned earlier. Consistent hashing helps distribute data across shards in a way that minimizes data movement and rebalancing when nodes are added or removed from the system.

# Closing Notes

In conclusion, understanding the differences between SQL and NoSQL databases, and the limitations of SQL databases in terms of scalability, replication, and sharding, helps in making informed decisions for designing robust systems.