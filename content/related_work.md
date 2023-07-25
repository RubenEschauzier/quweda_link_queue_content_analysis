## Related Work
{:#relatedwork}
In the LTQP literature, there is limited research into link prioritization approaches. 
<span class="comment" data-author="RV">Careful stating that as bluntly; it either means that we haven't done our homework, or that there is no research interest. I think there's some research indeed, especially among the pool of people who will read this paper, so careful not to step on their toes 🙂 It all depends on what you want to say. That research is urgent? That we're among the first? Think about what you really want to say, and say that—and perhaps the sentence can just go.</span>
The research focuses on querying the entire Web of linked data and does not assume any structural properties of the distributed environment. 
We will discuss [_graph-based_](cite:cites hartig2016walking), [_intermediate solution-based_](cite:cites hartig2016walking), and [_string similarity-based algorithms_](cite:cites lynden2013hybrid).

In [](cite:cites hartig2016walking), the authors introduce graph-based link prioritization. 
<span class="comment" data-author="RV">Avoid writing references in a way that impacts the text; i.e., you should be able to read the text aloud without having to say the numbers.</span>
These algorithms apply _vertex scoring_ methods to a dynamically constructed directed graph that represents the discovered topology of the Web. 
Each vertex denotes either a retrieved document or a queued URI, and directed edges represent that we obtain the URI of the target vertex from the source vertex's data. 
The authors use [_PageRank_](cite:cites page1998pagerank) and _Indegree-based scoring_ to calculate link priorities.
PageRank iteratively scores vertexes according to their importance, where more edges to a vertex will increase its importance, and edges from important vertexes have more weight. 
Indegree-based scoring counts the number of incoming edges of a vertex and uses this as its importance score.

[_Intermediate solutions-based link prioritization (ISLP)_](cite:cites hartig2016walking) is an adaptive approach where vertexes are scored based on the number of solutions the vertex has contributed to. 
ISLP then scores links based on the neighboring vertexes' scores.
 This approach uses the belief that highly relevant documents contain links to other relevant documents.
Finally, in [](cite:cites lynden2013hybrid), the authors prioritize URIs similar to previously dereferenced URIs that produced query results. 
<span class="comment" data-author="RV">idem</span>
For URI similarity, the authors use Levenshtein string distance.

For all approaches, the literature suggests that while link prioritization outperforms a simple FiFo queue for some queries, it performs worse for others.
We conclude that, while link prioritisation has merit, it needs more in-depth research into what makes a sound link prioritisation approach and why some queries show no benefit from link prioritisation and others do.

<span class="comment" data-author="RV">Good build-up in this section.</span>
