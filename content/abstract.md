## Abstract
<!-- Context      -->
Link Traversal-based Query Processing (LTQP) is a decentralized querying approach that iteratively follows links at runtime to discover data sources to query.
Given the dynamic nature of source discovery, query processing tends to be relatively slow.
<!-- Need         -->
Optimization techniques exist, such as exploiting existing structural information, but they depend on a deep understanding of the link queue during LTQP.
<!-- Task         -->
To this end,
we investigated the evolution of the types of link sources in the link queue,
and introduce a metric for link queue source type diversity during query execution, indicating the potential of source type-based link prioritisation as an optimization technique.
<!-- Object       -->
This paper discusses the possible effectiveness of link prioritisation algorithms that exploit existing structural information.
<!-- Findings     -->
Our results show that for some queries current link discovery methods are insufficient, while for other queries the bad query planning causes the slow query execution times.
<!-- Conclusion   -->
Based on our results, we conclude that research should focus both on more efficient or selective link traversal techniques and on improving query planning in LTQP.
<!-- Perspectives -->
Future research should therefore take into account that improving LTQP performance is a multi-fascetted problem that can not be solved by one silver bullet.
