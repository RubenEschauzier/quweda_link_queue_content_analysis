## Conclusion
{:#Conclusion}

In this paper, we investigate the contents of the link queue during LTQP over SOLID pods. 
Based on the content of the link queue during query execution, we divide queries into two types. 
The first query type (type one) has a primarily empty link queue during query execution. 
In contrast, the second query type (type two) has a link queue that fills rapidly, and the query engine cannot empty it quickly enough. 
For type one queries, the bottleneck is their query execution plan. 
This bottleneck shows that improving existing zero-knowledge query planning is required to optimize LTQP over the Solid environment. 
For type two queries, we find that while the link queue quickly fills up with links retrieved using cMatch, other link sources are often present concurrently.
These observations highlight that link prioritization based on the structural properties of Solid can influence query execution time and that the cMatch criterion is not sufficiently selective for efficient LTQP. 
We conclude that future work on LTQP for Solid has three avenues for research. 
Researchers should investigate new query optimization algorithms to improve type one query execution. 
Adaptive query planning seems especially promising due to the lack of prior knowledge of the data during LTQP. 
For type two queries, our analysis shows that link prioritization using the structural properties of the Solid system can influence query execution. 
Thus, future research into how to use these structural assumptions to prioritize links is an interesting future direction. 
Finally, the large number of cMatch sourced links in type two queries' link queue shows that using cMatch to discover new Solid pods is insufficiently selective. 
Future work should investigate alternative approaches that allow for more selective cross-pod link traversal.