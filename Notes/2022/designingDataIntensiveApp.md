# Designing Data-Intensive Applications

1. CPU clock speeds are barely increasing, but multicore processors are standard, and networks are getting faster. This means parallelism is only going to increase. 
2. Many application need to:
    - store data, find it again later(database)
    - remember the result of an expensive operation, to speed up reads(caches)
    - allow users to search data by keyword or filter it in various way(search indexes)
    - send a message to another process, to be handled asynchronously(stream processing)
    - periodically crunch a large amount of accumulated data(batch processing)
3. Average response time is not a very good metric if you want to know how many users actually experienced that delay. It is better to use percentiles. If you take a list of response times and sort it from fastes to slowest, the median(50th percentile, p50) is the halfway point, if your median response time is 200ms, that means half your requests return in less than 200ms, and half your requests take longer than that. 
4. An imperative language tells the computer to perform certain operations in a certain order, line by line, evaluating conditions, loop and etc.
5. A declarative query language, you just specify the pattern of the data you want(the final goal), but not how to achieve that goal. 
6. For writes, it's hard to beat the performance of simply appending to a file, any kind of index usually slow down writes, because the index also needs to be updated every time data is written. 
7. Sorted String Table(SSTable), key-value pair like prometheus counter, each key only appears once within merged segment file. First, append to the file(useful for recovery), merge the segment data is final data. 
8. Log-structured merged tree, LSM-Tree is typically faster for writes, whereas B-trees are thought to be faster for reads.
9. Transaction processing system(OLTP) vs Analytic system(OLAP)/Data Warehousing -> Column Oriented Storage(parquet) -> Column compression use bitmap.
10. Encoding and decoding. When you write data to a file or send it over the network, you have to encode it, also known as serialization or marshalling, reverse is called decoding(parsing, deserialization, unmarshalling.)
11. Binary encoding(facebook Thrift, google Protocol Buffers, Avro) can reduce the size. 
12. RPC drawbacks, local function call is predictable, the network request may lost, network slow and etc. It may return without a result, due to timeout, and you simply don't know whether request got through or not. If you retry a failed network request, that requests are actually getting through, only the responses are getting lost. The execution time might vary a lot due to network congestion. 
13. The main focus of RPC frameworks is on requests between services owned by the same organization, within the same datacenter. 
14. A message broker advantages:
    - act as a buffer
    - auto redeliver messages if failed before, prevent message from being lost.
    - sender doesn't need to know ip address or port number of the recipient
    - one message to be sent to several recipients.
    - decouples the sender from recipient, the sender just publishes message and doesn't care who consumes them. 
15. message broker compare to RPC, the communication is usually one way, a sender doesn't expect to receive a reply. 
16. Database replication, leaders and followers
    - if synchronous follower crashed, network fault, the write cannot be processed. The leader must block all writes and wait. It is impractical for all followers to be synchronous, it usually one of the followers is synchronous and the others are asynchronous. 
    - failover, one followers need to be promoted to be the new leader, clients need to be reconfigured to send their writes to the new leader, the other followers need to start consuming data changes from the new leader. When old leader back online, he need to step down as a follower and recognize the new leader, deal with data mismatch. 
17. Monotonic reads means that if one user makes several reads in sequence, they will not read older data after having previously read newer data.
18. Use cases for multi leader replication -> multi-datacenter operation, better performance, tolerance of datacenter outages and network problem, however need to handling write conflicts. 
19. Leaderless Replication, (e.g. AWS Dynamo, Casssandra), no failover, read/write parallel from multiple nodes, are generally optimized for usse cases that can tolerate eventual consistency. Quorums(法定人数) for reading and writing. write = read = nodes/2 + 1 
20. For defining concurrency, exact time doesn't matter, if two operations are both unaware of each other, we call it concurrency. 
21. CAP theorem: consistency, availability, partition tolerance. When you have a distributed system(partition), it is never safe from network failures, thus they aren't something about which you have a choice: network failure will happen whether you like it or not. If some nodes are not available or there is network communication issue between the nodes, you have to choose between consistency and availability. "two out of three" concept can be somewhat misleading because system designers need only to sacrifice consistency or availability in the presence of partitions
22. The advantage of a global(term-partitioned) index over a document-partitioned index is that it can make reads more efficient: rather than doing scatter/gather over all partitions, a client only needs to make a request to the partition containing the term that it wants. However, the downside of a global index is that writes are slower and more complicated. 
23. Fixed number of partitions: create many more partitions than there are nodes, and assign several partitions to each node, if a node is added to the cluster, the new node can steal a few partitions from every existing node. 
24. ZooKeeper, many distributed data systems rely on a separate coordination service to keep track cluster metadata, each node registers itself in ZooKeeper, and ZooKeeper maintains the mapping of partitions to nodes. When a partition changes ownership, or a node is added or removed, it can also notifies the routing tier so that it can keep its routing information up to date. 
25. A transaction is a way for an application to group several reads and writes together into a logical unit. 
26. Durability mean that the data has been successfully copied to some number of nodes. In order to provide a durability guarantee, a database must wait until these writes or replications are complete before reporting a transaction as successfully committed. 
27. Executing transactions serially is implemented in VoltDB, Redis. A system designed for single-threaded execution can sometimes perform better than a system that supports concurrency, because it can avoid the coordination overhead of locking. 
28. Linearizability: the basic idea is to make a system appear as if there were only one copy of the data, and all operations on it are atomic. With this guarantee, even though there may be multiple replicas in reality, the application does not need to worry about them. However, linearizability is slow and this is true all the time, not only during a network fault. Linearizability implies/ensures causality(因果) and it is not the only way of preserving causality, A system can be causally consistent without incurring the performance hit of making it linearizable. In fact, causal consistency is the strongest possible consistency model that does not slow down due to network delays, and remains available in the face of network failures. 
29. The best-known fault-tolerant consensus algorithms are Viewstamped Replication(VSR), Paxos, Raft and Zab.
30. check these useful linux command awk, sed, sort, uniq, xargs
31. Sushi principle: raw data is better
32. For pub/sub model consider two questions: what happens if producers send faster than consumers can process them(drop, buffer in a queue, backpressure). What happens if nodes crash or offline, are any messages lost(durability)?
33. Message brokers vs databases:
    - database usually keep the data until it is explicitly deleted. Message broker not for long-term data storage
    - database support secondary indexes and various ways of searching for data. Message brokers support subscribing to a subset of topics matching some pattern. 
    - query database, the result is a point-in-time snapshot. Message broker will keep notify you when data changes. 
34. When multiple consumers read messages in the same topic, two main patterns are used: load balancing or Fan-out
35. Even if the message broker tries to preserve the order of messages, the combination of load balancing with redelivery inevitably leads to messages being reordered. 
36. 

