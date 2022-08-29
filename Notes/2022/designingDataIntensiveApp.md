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
