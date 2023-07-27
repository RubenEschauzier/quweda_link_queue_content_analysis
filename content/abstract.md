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
This paper analyses the link queue to guide future work on LTQP query optimization approaches that exploit structural information within a Solid environment.
<!-- Findings     -->
Our results show that queries exhibit two different execution patterns:
one where the link queue is primarily empty,
and the other where the link queue fills faster than the engine can process. 
<!-- Conclusion   -->

This dichotomy shows that LTQP is a multifaceted problem and needs to be approached from different research directions.
<span class="comment" data-author="RV">I don't see how the multifaceted follows from the dichotomy; maybe the argument is detailed in the paper, but then I would phrase as:
<q>We explain how this dichotomy indicates that LTQP is a multifaceted problem…</q>
</span>
<span class="comment" data-author="RV">Although, if I'm honest, I don't really like this multifaceted conclusion. On the one hand, it's something we already knew (so nothing new learned here); on the other hand, it's true in general, many things are multifaceted, so what does it _really_ mean?</span>
We conclude that LTQP optimization research should focus on more efficient or selective link traversal techniques and improving query planning in LTQP.
<span class="comment" data-author="RV">Well, we already knew that too. So that's not really a conclusion. I think a conclusion is that the link queue is not functioning optimally, and that investigating into different kinds of backlogs might be needed. Maybe that is multiple queues, maybe that is prioritized queues, maybe…</span>
