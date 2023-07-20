## Related Work
{:#relatedwork}
In the LTQP literature, there is limited research into link prioritization approaches. 
The research focuses on querying the entire Web of linked data and does not assume any structural properties of the distributed environment. 
We will discuss graph-based [](cite:cites hartig2016walking), intermediate solution-based [](cite:cites hartig2016walking), and string similarity-based algorithms [](cite:cites lynden2013hybrid). \\
In [](cite:cites hartig2016walking), the authors introduce graph-based link prioritization. 
These algorithms apply vertex scoring methods to a dynamically constructed directed graph that represents the discovered topology of the Web. 
Each vertex denotes either a retrieved document or a queued URI, and directed edges represent that we obtain the URI of the target vertex from the source vertex's data. 
The authors use PageRank [](cite:cites page1998pagerank) and Indegree-based scoring to calculate link priorities.
PageRank iteratively scores vertexes according to their importance, where more edges to a vertex will increase its importance, and edges from important vertexes have more weight. 
Indegree-based scoring counts the number of incoming edges of a vertex and uses this as its importance score. \\
Intermediate solutions-based link prioritization (ISLP) [](cite:cites hartig2016walking) is an adaptive approach where vertexes are scored based on the number of solutions the vertex has contributed to. 
ISLP then scores links based on the neighboring vertexes' scores.
 This approach uses the belief that highly relevant documents contain links to other relevant documents. \\
Finally, in [](cite:cites lynden2013hybrid), the authors prioritize URIs similar to previously dereferenced URIs that produced query results. 
For URI similarity, the authors use Levenshtein string distance. \\
For all approaches, the literature suggests that while link prioritization outperforms a simple FiFo queue for some queries, it performs worse for others.
From this, we conclude that while link prioritisation has merit, it needs more indepth research into what makes a sound link prioritisation approach and why some queries show no benefit from link prioritisation and others do.

