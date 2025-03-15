# Homework 16

##### Question #1:

What are some limitations you can see with cache-backed embeddings approach? When is this most/least useful. Discuss with your group!

Limitations of the cache-backed embeddings approach used in the provided code. 

##### Limitations:

##### Cache Size and Management:
Storing embeddings for every document can consume a significant amount of memory, especially for large datasets. Hence, if the cache becomes too large, it can lead to performance issues or even crashes. Efficient cache management strategies, such as eviction policies, are necessary.
##### Cache Invalidation:
If the underlying data or embeddings model is updated, the cached embeddings may become outdated. Using stale embeddings can result in inaccurate retrieval results. Implementing a mechanism to invalidate and update the cache becomes very important
##### Cold Start Problem:
When the cache is empty, the initial embedding process for a new document will still require a full API call, incurring latency. This can be noticeable for the first few queries or when dealing with frequently changing datasets.
##### Limited Scalability for Distributed Systems:
The current implementation uses a LocalFileStore for caching, which might not be suitable for distributed environments where multiple Colab instances or workers need to share the cache. In such cases, a centralized and distributed cache, like Redis, would be more appropriate.
##### Data Consistency:
In distributed setups, ensuring consistency between the cache and the vector database (QDrant in this case) can be challenging. If data is updated in the vector database but not reflected in the cache, it can lead to inconsistencies and incorrect results.

##### Question #2:

What are some limitations you can see with prompt caching approach? When is this most/least useful. Discuss with your group!

Limitations of the prompt caching approach used in the provided code. 

##### Limitations:

##### Cache Size and Management:
Storing the responses for every prompt can consume a lot of memory, especially if you have a wide variety of prompts and responses. This can lead to performance issues if the cache becomes too large. Consider using a cache with eviction policies (like LRU) to manage its size effectively.

##### Limited Context Awareness:
The current InMemoryCache implementation doesn't consider the context of the conversation or previous interactions. If a prompt is similar but used in a different context, the cached response might be inaccurate or irrelevant. More advanced caching mechanisms might need to consider the conversation history for better accuracy.

##### Cache Invalidation:
If the underlying LLM model or its behavior is updated, the cached responses might become outdated. This can lead to inconsistencies and potentially incorrect answers. Consider implementing strategies to invalidate or update the cache periodically or when the LLM is updated.

##### Data Consistency in Distributed Environments:
If you're using multiple Colab instances or workers in a distributed setup, ensuring consistency between the caches can be challenging. This might result in different instances using different cached responses for the same prompt, leading to inconsistencies. Consider a centralized or distributed caching solution for such scenarios.

##### Potential for Bias and Inappropriate Content:
Cached responses might reflect the biases or inappropriate content present in the original LLM output. It's essential to review and filter cached responses to mitigate these risks, especially in sensitive applications.


