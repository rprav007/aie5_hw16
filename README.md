# Homework 16

##### ❓ Question #1:

What are some limitations you can see with this approach? When is this most/least useful. Discuss with your group!

Limitations of the cache-backed embeddings approach used in the provided code. 

**Limitations:

Cache Size and Management:
Reasoning: Storing embeddings for every document can consume a significant amount of memory, especially for large datasets.
Impact: If the cache becomes too large, it can lead to performance issues or even crashes. Efficient cache management strategies, such as eviction policies, are necessary.
Cache Invalidation:
Reasoning: If the underlying data or embeddings model is updated, the cached embeddings may become outdated.
Impact: Using stale embeddings can result in inaccurate retrieval results. Implementing a mechanism to invalidate and update the cache is crucial.
Cold Start Problem:
Reasoning: When the cache is empty, the initial embedding process for a new document will still require a full API call, incurring latency.
Impact: This can be noticeable for the first few queries or when dealing with frequently changing datasets.
Limited Scalability for Distributed Systems:
Reasoning: The current implementation uses a LocalFileStore for caching, which might not be suitable for distributed environments where multiple Colab instances or workers need to share the cache.
Impact: In such cases, a centralized and distributed cache, like Redis, would be more appropriate.
Data Consistency:
Reasoning: In distributed setups, ensuring consistency between the cache and the vector database (QDrant in this case) can be challenging.
Impact: If data is updated in the vector database but not reflected in the cache, it can lead to inconsistencies and incorrect results.
