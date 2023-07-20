## Abstract
<!-- Context      -->
Link Traversal-based Query Processing (LTQP) is a decentralized querying approach that iteratively follows links at runtime to discover data sources to query.
Given the dynamic nature of source discovery, query processing tends to be relatively slow.
<!-- Need         -->
Optimization techniques exist, such as exploiting existing structural information, but they depend on a deep understanding of the link queue during LTQP.
<!-- Task         -->
To this end,
we investigate the evolution of the types of link sources in the link queue and introduce metrics that describe key link queue characteristics. 
<!-- Object       -->
This paper analyses the link queue to guide future work on LTQP query optimization approaches that exploit structural information of the Solid environment.
<!-- Findings     -->
Our results show that queries exhibit two different execution patterns, one where the link queue is primarily empty and the other where the link queue fills faster than the engine can process. 
This dichotomy shows that LTQP is a multifaceted problem and needs to be approached from different research directions.
<!-- Conclusion   -->
We conclude that LTQP optimization research should focus on more efficient or selective link traversal techniques and improving query planning in LTQP.