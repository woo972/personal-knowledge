---
tags:
  - dev
  - cache
  - policy
  - redis
---
## Basic Principle for cache
---
- Only the hot data(business critical, latency is important) should be put into the cache
- The closer to the final calculation result, the more valuable
- For the cache that needs to consume I/O resources, the number of calls should be reduced as much as possible.
- All cached information shall be set with expiration time
- Cache expiration time should be dispersed to avoid centralized expiration
- Ensure that the data written to the cache is complete and correct
- Select the appropriate data structure
	- The cache key should be readable
	- Cache keys with the same name should be avoided for different services
	- Key can be appropriately abbreviated to save memory space
	- The data corresponding to a key should not be too large
	- For string type, the value size corresponding to a key should be controlled within 10K, and about 1K is better
	- Hash type, no more than 5000 lines
- In the default redis configuration, if the operation takes more than 10ms, it is regarded as a slow query
- Avoid using long-time operation commands, such as: keys *
- Have cache preheating
	- For applications that may have a large number of read requests after going online, the data can be written to the cache in advance before going online
- Avoid cache penetration 
	- For the data not queried in the database, a special ID can be set to avoid every request reaching the database because there is no data in the cache
	- If some nonexistent data is continuously requested due to inappropriate business or malicious attacks, all requests will fall on the database because the cache does not save the data, which will cause great pressure on the database or even collapse. A simple countermeasure is to cache nonexistent data.
	- In order to avoid invalid data occupying the cache, we usually do not store empty objects in the cache, but this strategy will cause cache penetration problems.
	- If the data to be queried does not exist, of course, it is impossible to find the data from the cache. According to the logic of cache miss, that is, accessing the database, all queries for nonexistent data will reach the database. This phenomenon is called cache penetration.
	- To reduce meaningless database access, we can cache placeholders indicating that the data does not exist.
	- Generally speaking, accessing deleted objects causes a high probability of cache penetration. Therefore, when deleting data, place placeholders in the cache to indicate that they have been deleted.
- The order of reading is cache first, then database. The order of writing is database first, then cache.
- The cache should have a degradation scheme. If there is a problem with the cache, it should be able to go back to the source database for processing
- Data consistency problem: when the data source is changed, the data in the cache may be inconsistent with the data in the data source. An appropriate cache update strategy should be selected according to the actual business needs
	- When writing data: write the database first, and then write the cache
	- When updating data: delete the cache first, then update the database, and finally write to the cache
	- When deleting data: delete the cache first, and then delete the database
	- When reading data: read the cache first. If there is no cache, read the database and update the cache