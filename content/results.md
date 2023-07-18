## Results
{:#results}

First we will present a selection of the link queue evolutions that accuractely represent what we found in all 27 queries. These figures are given in [](#figure-main), each of these figures has the query execution time on the x-axis, and the number of links on the y-axis. We run the queries using the default SOLID configuration of Comunica [](cite:cites taelman2018comunica) and we set the time-out at 60 seconds, however this is not a strict time-out as it can run longer due to implementation details. From these figures, we find two categories of queries: queries where the number of links followed is easily processed by the query engine and queries where the number of links followed increases steadily and the query engine cannot handle the number of discovered links. 
Furthermore, we set the time-out to 1100 seconds for [](#figure-main-5) to investigate the spike of cMatch links. In [](#figure-main-6) we find that the cMatch criterion can quickly generatea massive number of links to follow, slowing down the query execution and making the query infeasible to execute.


<figure id="figure-main" class="result-figure-grid ">

<figure id="figure-main-1" class="subfigure">
<img src="figures/interactive-complex-3-timestamps.svg">
<figcaption markdown="block">
Link queue content of the complex-3 query. 
</figcaption>
</figure>

<figure id="figure-main-2" class="subfigure">
<img src="figures/interactive-discover-7-timestamps.svg">
<figcaption markdown="block">
Link queue content of the discover-7 query. 
</figcaption>
</figure>

<figure id="figure-main-3" class="subfigure">
<img src="figures/interactive-short-2-timestamps.svg">
<figcaption markdown="block">
Link queue content of the short-2 Query. 
</figcaption>
</figure>

<figure id="figure-main-4" class="subfigure">
<img src="figures/interactive-short-7-timestamps.svg">
<figcaption markdown="block">
Link queue content of the short-7 query. 
</figcaption>
</figure>

<figure id="figure-main-5" class="subfigure">
<img src="figures/interactive-complex-2-timestamps-shortened.svg">
<figcaption markdown="block">
Link queue content of the complex-2 query.
</figcaption>
</figure>
<figure id="figure-main-6" class="subfigure">
<img src="figures/interactive-complex-2-timestamps.svg">
<figcaption markdown="block">
Link queue content of the complex-2 query with extended timeout. 
</figcaption>
</figure>
</figure>

To quantify the two different types of query categories, we investigate the metrics introduced in [](#experimentsetup). We split the queries into two categories, one with links in the queue for more than 50% of the query execution time and the other less than 50%. The group with high queue occupancy contains twelve queries, while the other group contains fifteen queries. The average metrics of the groups are given in [](#tab:metrics). 

<figure id="tab:metrics" class="table" markdown="1">

| Query Category | %cMatch | %Contains |pEff(2) | pEff(1) | $$\bar{n^{q}}(0)$$ | $$\bar{n^{q}}(1)$$ |
|---|---|---|---|---|---|---|
| High Queue Occupancy | 0.535 | 0.265 | 0.447 | 0.815 | 2.14 | 2.445 |
| Low Queue Occupancy | 0.290 | 0.423 | 0.019 | 0.118 | 0.137 | 1.134 |

<figcaption markdown="block">
Average metrics for queries with more than 50% Link Queue Occupancy, and for smaller than 50%. Here **%cMatch** denotes the percentage of links that have cMatch as source, **%Contains** for links with Contains predicates as source. **pEff(k)** denotes the percentage of time the queue has $k$ or more links in it. Finally, **$$\bar{n^{q}}(k)$$** the average number of links in the queue, when atleast $$k$$ links are in the queue. 
</figcaption>
</figure>



## Discussion
{:#Discussion}

As mentioned, we find that we can visually divide queries into two subgroups. Queries where the link queue is mainly empty and the query planning forms the bottleneck, and queries where the link queue fills up rapidly and the query engine cannot dereference the links quick enough. This visual analysis is supported by the metrics. By dividing the queries based on the percentage of time the link queue has atleast one entry in it, we find a clear difference in link queue characteristic metrics. We see that queries with high queue occupancy have a larger percentage of *cMatch* links and on average have more thank one type of link in the queue for 50% of the query execution time. On the other hand, queries with low queue occupancy have a higher occurence rate of *contains* links and almost never have more than two types of links in the queue at the same time.
The queries where the link queue is primarily empty, support the conclusion of [](cite:cites taelman2023evaluation). In this paper they conclude that current query plan optimization approaches are perform poorly for LTQP. When the link queue is empty, but the query times-out, we know that this timeout is caused by the execution of the query over the retrieved data, not the time spent dereferencing URIs.
Furthermore, we find that for the queries with too many links to follow, these links are mainly produced by links discovered using the cMatch criterion. The cMatch criterion is primarily used to discover other SOLID pods, as for a query over a single solid pod all data can be found by dereferencing the contains and storage predicate links. Queries where the link queue fills up with thousands of cMatch sourced links shows that this method of pod discover is not sufficiently selective. Indeed, for these queries it might be required to find a way to discover other pods that is more selective and doesn't produce the gigantic amount of followable links like cMatch does. 