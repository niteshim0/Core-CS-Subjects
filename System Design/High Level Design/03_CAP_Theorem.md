# CAP Theorem

The CAP theorem, also known as Brewer's theorem, is a fundamental principle in distributed systems architecture, proposed by Eric Brewer in 2000 and formally proven in 2002. It states that a distributed system can only provide at most two out of the following three guarantees simultaneously:

`Desirable properties of a distributed system with replicated data`

![CAP Theorem](https://hazelcast.com/wp-content/uploads/2021/12/cap-theorem-diagram-800x753-1.png)

1. **Consistency (C)**: Every read receives the most recent write or an error. This ensures that all nodes in the system see the same data at the same time.
   
2. **Availability (A)**: Every request (read or write) receives a response, without guarantee that it contains the most recent write. This ensures that the system remains operational and responsive.
   
3. **Partition Tolerance (P)**: The system continues to operate despite network partitions. This means that the system can sustain network failures that split the system into two or more disjoint sets of nodes.

## Implications of the CAP Theorem

- **CP Systems** (Consistency and Partition Tolerance):
  - These systems prioritize consistency over availability. They ensure that all nodes have the same data but may become unavailable during network partitions.
  - Example: HBase, MongoDB (in certain configurations)

- **AP Systems** (Availability and Partition Tolerance):
  - These systems prioritize availability over consistency. They provide the most recent data available even if it might be stale and can tolerate network partitions.
  - Example: Couchbase, DynamoDB

- **CA Systems** (Consistency and Availability):
  - These systems theoretically prioritize both consistency and availability but do not tolerate network partitions well.
  - Example: Traditional relational databases like MySQL (though not typically considered distributed)

## Understanding Trade-offs

- **Consistency vs. Availability**: The CAP theorem forces a choice between ensuring every read receives the most recent write (consistency) and ensuring every request receives a response (availability).
- **Partition Tolerance**: Given that network partitions are inevitable in distributed systems, systems must choose how to handle them, typically by sacrificing either consistency or availability.

The CAP theorem highlights the inherent trade-offs in distributed systems. While it is impossible to achieve all three guarantees simultaneously, understanding the requirements of your application can help in choosing the right balance between consistency, availability, and partition tolerance. This, in turn, guides the design and implementation of distributed databases and other systems.
