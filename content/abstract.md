## Abstract
<!-- Context      -->
Link Traversal-based Query Processing (LTQP) is an integrated querying approach that allows the query engine to start with zero knowledge of the data to query and discover data sources on the fly.
The query engine starts with some seed documents and dynamically discovers new data sources by dereferencing hyperlinks in previously ingested data.
Given the dynamic nature of source discovery, query processing tends to be relatively slow.
Optimization techniques exist, such as exploiting existing structural information, 
<!-- Need         -->
but they depend on a deep understanding of the link queue during LTQP.
<!-- Task         -->
To this end,
we investigate the evolution of the types of link sources in the link queue and introduce metrics that describe key link queue characteristics. 
<!-- Object       -->
This paper analyses the link queue to guide future work on LTQP query optimization approaches that exploit structural information within a Solid environment.
<!-- Findings     -->
Our results show that queries exhibit two different execution patterns,
one where the link queue is primarily empty
and the other where the link queue fills faster than the engine can process. 
<!-- Conclusion   -->
Our results show that the link queue is not functioning optimally and that our current approach to link discovery is not sufficiently selective. 
