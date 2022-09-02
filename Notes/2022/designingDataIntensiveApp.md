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
    - 

