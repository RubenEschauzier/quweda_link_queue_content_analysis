## Conclusion
{:#Conclusion}

In this paper, we investigated the contents of the link queue during LTQP over Solid pods. 
Based on the content of the link queue during query execution, we divide queries into two types. 
The first query type has a primarily empty link queue during query execution. 
In contrast, the second query type has a link queue that fills rapidly, and the query engine cannot empty it quickly enough. 
For low queue occupancy queries, the bottleneck is their query execution plan. 
This bottleneck shows that improving existing zero-knowledge query planning is required to optimize LTQP over the Solid environment. 
For high queue occupancy queries, we find that while the link queue quickly fills up with links retrieved using <em class="keyword">cMatch</em>, other link sources are often present concurrently.

These observations highlight that _link prioritization_ based on the structural properties of Solid can influence query execution time and that the <em class="keyword">cMatch</em> criterion is not sufficiently selective for efficient LTQP. 
We conclude that future work on LTQP has three avenues for research:

- Investigate new query optimization algorithms to improve low queue occupancy query execution. 
Adaptive query planning seems especially promising due to the lack of prior knowledge of the data during LTQP. 
- For high queue occupancy queries, our analysis shows that link prioritization using the structural properties of the Solid system can influence query execution. 
Thus, future research into how to use these structural assumptions to prioritize links is an interesting future direction. 
- Finally, the large number of <em class="keyword">cMatch</em> sourced links in the link queue of high queue occupancy queries show, that using <em class="keyword">cMatch</em> to discover new Solid pods is insufficiently selective. 
Future work should investigate alternative approaches that allow for more selective cross-pod link traversal.

### Acknowledgements
This research was supported by SolidLab Vlaanderen (Flemish Government, EWI and RRF project VV023/10).
Ruben Taelman is a postdoctoral researcher at the Research Foundation – Flanders (FWO).

<div style="page-break-after: always;"></div>
