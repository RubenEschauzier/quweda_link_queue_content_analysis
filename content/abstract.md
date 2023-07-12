## Abstract
<!-- Context      -->
Link Traversal-based Query Processing (LTQP) is a decentralized querying approach that requires no prior information on the location of data sources.
LTQP iteratively follows links found in dereferenced data to discover data sources to query.
<span class="comment" data-author="RV">Try to keep context short; it's not the exciting bit. Suggestion to combine the previous 2 sentences into 1.</span>
<!-- Need         -->
However, <span class="rephrase" data-author="RV">this</span> significantly slows down query execution.
To improve <span class="rephrase" data-author="RV">usability</span>,
<span class="comment" data-author="RV">I think you mean <q>usefulness</q>, but there's a more fitting concept surely.</span>
we need to reduce total query execution time or produce initial results faster in a streaming fashion.
<del class="comment" data-author="RV">Faster initial results allows applications to present first results more quickly and improve responsiveness of applications.</del>
<span class="comment" data-author="RV">That should be given.</span>
When we consider decentralized environments with known structural properties, such as is the case with Solid pods, we can use these properties to prioritize data sources that are likely relevant to the query.
<span class="comment" data-author="RV">What I'm going to say here is difficult, but the previous sentence should more or less be the second—at most third—sentence of your abstract. All the rest is context, but this is where we start explaining what's new. You can keep the rest for intro, but abstract has to jump to the point.</span>
Prioritizing relevant data sources can improve initial <var>k</var> query result arrival times.
However, before we develop complex algorithms to find an optimal link prioritization strategy, it is vital to analyze what happens inside the link queue during LTQP.
<span class="comment" data-author="RV">And maybe even the previous sentence should be the third one.</span>
<!-- Task         -->
<del class="comment" data-author="RV">We analyzed the potential of link prioritization using structural assumptions by using solid as a test case.</del>
We investigated the evolution of the types of link sources in the link queue and introduce a metric for link queue source type diversity during query execution. 
<!-- Object       -->
<del class="comment" data-author="RV">Finally, we discuss future work for link prioritization.</del>
<span class="comment" data-author="RV">The abstract is not necessarily a summary nor a structural overview; it's more like quick breakdown of what you'll find.</span>
<ins class="comment" data-author="RV">Explain here what the current paper offers (which likely is a description of your tasks of the outcome thereof)</ins>
<!-- Findings     -->
<span class="todo">Still need findings, conclusion, and perspectives. Will do after I get the plots.</span>
<!-- Conclusion   -->
<!-- Perspectives -->

<span class="comment" data-author="RV">Quickly trying an abstract below where I get to the meat in sentence 2/3. Just as inspiration; do as you see fit.</span>

<!-- Context      -->
Link Traversal-based Query Processing (LTQP) is a decentralized querying approach that iteratively follows links at runtime to discover data sources to query.
Given the dynamic nature of source discovery, query processing tends to be relatively slow.
<!-- Need         -->
Optimization techniques exist, such as exploiting existing structural information, but they depend on a deep understanding of the link queue during LTQP.
<!-- Task         -->
To this end,
we investigated the evolution of the types of link sources in the link queue,
and introduce a metric for link queue source type diversity during query execution.
<span class="comment" data-author="RV">Assuming that diversity is good or bad here? Be explicit, because I genuinely don't know 🙂</span>
<!-- Object       -->
This paper discusses <span class="todo"></span>.
<!-- Findings     -->
Our results show that <span class="todo"></span>.
<!-- Conclusion   -->
Based on those results, we conclude that <span class="todo"></span>.
<!-- Perspectives -->
Future research should therefore focus on / take into account <span class="todo"></span>.
