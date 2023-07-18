## Related Work
{:#relatedwork}
In the LTQP literature there is limited existing research into link prioritization approaches. The research that does exist focuses on querying the entire web of linked data and does not assume any structural properities of the distributed environment. We will discuss graph-based [](cite:cites hartig2016walking), intermediate solution-based [](cite:cites hartig2016walking), and string similarity-based algorithms [](cite:cites lynden2013hybrid). \\
In [](cite:cites hartig2016walking), the authors introduce graph-based link prioritisation. These algorithms apply vertex scoring methods to a dynamically constructed directed graph that represents the discovered topology of the Web. Each vertex denotes either a retrieved document or a queued URI and each directed edge represents that the receiving vertex was found using a URI in the data of the source vertex. On this graph they use PageRank [](cite:cites page1998pagerank) and Indegree-based scoring. PageRank iteratively scores vertexes according to their importance, where, very simply said, more edges to a vertex will increase its importance and edges from important vertexes hold more weight. Indegree-based scoring counts the number of incoming edges of a vertex and uses this as its importance score.

Intermediate solutions-based link priorisiation [](cite:cites hartig2016walking) is an adaptive approach where vertexes are scored based on the number of intermediate results they produce.

Finally, in [] they use a string similarity based measure

