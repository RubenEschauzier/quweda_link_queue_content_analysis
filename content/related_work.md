## Related Work
{:#relatedwork}
In LTQP literature, the focus is on querying the entire Web of linked data without any assumptions on the structural properties of the distributed environment. 
We will discuss [_graph-based_](cite:cites hartig2016walking), [_intermediate solution-based_](cite:cites hartig2016walking), and [_string similarity-based algorithms_](cite:cites lynden2013hybrid).

<!-- In [](cite:cites hartig2016walking), the authors introduce graph-based link prioritization. 
<span class="comment" data-author="RV">Avoid writing references in a way that impacts the text; i.e., you should be able to read the text aloud without having to say the numbers.</span> -->
[_Graph-based link prioritization_](cite:cites hartig2016walking) applies _vertex scoring_ methods to a dynamically constructed directed graph that represents the discovered topology of the Web. 
Each vertex denotes either a retrieved document or a queued URI, and directed edges represent that we obtain the URI of the target vertex from the source vertex's data. 
The authors use [_PageRank_](cite:cites page1998pagerank) and _Indegree-based scoring_ to calculate link priorities.
PageRank iteratively scores vertexes according to their importance, where more edges to a vertex will increase its importance, and edges from important vertexes have more weight. 
Indegree-based scoring counts the number of incoming edges of a vertex and uses this as its importance score.

[_Intermediate solutions-based link prioritization (ISLP)_](cite:cites hartig2016walking) is an adaptive approach where vertexes are scored based on the number of solutions the vertex has contributed to. 
ISLP then scores links based on the neighboring vertexes' scores.
This approach uses the belief that highly relevant documents contain links to other relevant documents. [_String similarity-based algorithms_](cite:cites lynden2013hybrid) also use this assumption. The algorithm prioritize URIs similar to previously dereferenced URIs that produced query results. To measure URI similarity, the authors use Levenshtein string distance.

For all approaches, the literature suggests that while link prioritization outperforms a simple FiFo queue for some queries, it performs worse for others.
We conclude that, while link prioritisation has merit, it needs more in-depth research into what makes a sound link prioritisation approach and why some queries show no benefit from link prioritisation and others do.
