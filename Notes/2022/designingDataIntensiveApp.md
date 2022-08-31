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
11. Binary encoding(facebook Thrift, google Protocol Buffers) can reduce the size. 
12. 
