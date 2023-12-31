## Experimental Setup
{:#experimental-setup}

In this section, we first describe the data we use for our analysis.
We then introduce the possible link types we can track in the Solid environment and how we measure the link queue evolution.
Finally, we introduce metrics to represent the diversity of links in the queue. 

### Data
{:##Data}

We use the recently introduced [_SolidBench benchmark_](cite:cites taelman2023evaluation) for our analysis, 
which uses the [_Social Network Benchmark (SNB)_](cite:cites angles2020ldbc, erling2015ldbc) at its core. 
The SNB models a social network similar to Facebook; social networks produce networks of connected data with users acting as data hubs.
This data structure is suited for the Solid protocol, where Solid pods act as data hubs.
SolidBench uses this centralized benchmark as a data generator and then fragments this data into data vaults, which function as Solid pods. 
We use the default data generation and fragmentation parameters, which results in 158,233 RDF files over 1,531 data vaults using the default fragmentation strategy.
There are 3,556,159 triples across all files, with 22.47 triples per file on average.

The SolidBench benchmark uses the read-only interactive workload of SNB, which corresponds to the workload that social network applications encounter. 
The interactive workload of SNB has two query template classes: _complex_ and _short_. 
[Preliminary testing](cite:cites taelman2023evaluation) of the benchmark show that these queries are challenging for existing LTQP techniques, with most complex queries reaching timeout. 
SolidBench includes _discover queries_ as a third query template class to enhance SNB.
These queries include various choke points in the dataset, like _multi-hop document traversal_, _type index_ usage, and determining what HTTP requests are irrelevant. 
The SolidBench workload consists of 27 query templates, for which we instantiate one query each. 

### Link Types in the Solid Ecosystem
{:##Link Types in the Solid Ecosystem}

In the Solid ecosystem, there are multiple predicates that serve a distinct function and result from the structural properties of the ecosystem. 
For example, _LDP Basic Containers_ serve as folders that contain references to documents or other LDP containers, while _type indexes_ denote a direct link to a resource in the vault with a type or class, like comments or posts.
For a more in-depth explanation of the Solid environment and its structural properties, we refer to [](cite:cites taelman2023evaluation). 
In [](#tab:priorities), we show all considered predicate types and the short versions of their name. 
Note the presence of <em class="keyword">cMatch</em>, the reachability criterion described in [](cite:cites hartig2012foundations).
We do not consider the <em class="keyword">cAll</em> criterion, as it will lead to an impractical number of followed links. 
When we dereference a URI, we can record whether we discover this URI from a triple with one of the previously mentioned predicates, thus giving us information on the type of document we are dereferencing. 

<figure id="tab:priorities" class="table" markdown="1">

| Link Source                                               | Short name                        |
| --------------------------------------------------------- | --------------------------------- |
| Type Index                                                | <em class="keyword">Type</em>     |
| <code>http://www.w3.org/ns/ldp#contains</code>            | <em class="keyword">Contains</em> |
| <code>http://www.w3.org/ns/pim/space#storage</code>       | <em class="keyword">Storage</em>  |
| <em class="keyword">cMatch</em> (reachability criterion)  | <em class="keyword">cMatch</em>   |
| <code>http://www.w3.org/2000/01/rdf-schema#seeAlso</code> | <em class="keyword">SeeAlso</em>  |
| <code>http://www.w3.org/2002/07/owl#sameAs</code>         | <em class="keyword">SameAs</em>   |
| <code>http://xmlns.com/foaf/0.1/isPrimaryTopicOf</code>   | <em class="keyword">TopicOf</em>  |

<figcaption markdown="block">
The different predicates or criteria used to discover new links in Link Traversal-based Query Processing over Solid.
</figcaption>
</figure>

### Link Queue Analysis
{:##linkqueueanalysis}

To investigate the behavior of the link queue during LTQP, we will register the link source for each dereferenced link during query execution. 
We make a snapshot of the link sources in the link queue whenever a link is popped from or pushed to the link queue and register the timestamp of the snapshot. 
Thus, we obtain the evolution of the sources in the link queue during query execution. 

Using this information, we will first plot the different types of sources and their numbers present in the link queue. 
This plot will give us an understanding of the data discovery pattern of the query engine and allow us to investigate avenues for link prioritization algorithms or other forms of optimization. 

To support the visual analysis of the link queue, we introduce metrics that measure link queue characteristics. 
We are interested in what percentage of all links we obtain from a given source. 
Furthermore, we will determine the fraction of time the link queue contains $$k$$ or more links ($$ p\mathit{Eff}(k) $$) and calculate the average number of link types present in the link queue, given $$k$$ links are present ($$\bar{n^{q}}(k)$$). 
These metrics give us insight into possible bottlenecks during query execution and whether link prioritization based on link sources has merit for LTQP.
We calculate these metrics using

$$
\begin{aligned}
    p\mathit{Eff}(k) = \dfrac{\sum_{\{t_{0} \leq t_{i} < t_{N}| n^{q}_{t_{i}} \geq k\}} t_{i+1} - t_{i}}{t_{n} - t_{0}}, \quad 
    \bar{n^{q}}(k) = \dfrac{\sum_{\{t_{0} \leq t_{i} < t_{N}|n^{q}_{t_{i}} \geq k\}} (t_{i+1} - t_{i})n^{q}_{t_{i}}}{t_{n} - t_{0}}. \\
\end{aligned}
$$

With $$t_{0}$$ the first timestamp recorded, $$t_{N}$$ the final timestamp, and $$n^{q}_{t_{i}}$$ the number of different link sources in the queue at timestamp $$t_{i}$$.
We execute the queries using Comunica [](cite:cites taelman2018comunica). Comunica uses the algorithm described in [](cite:cites taelman2023evaluation), which uses a FiFo link queue and set the query timeout to 60 seconds. All code for [running the experiment](https://github.com/RubenEschauzier/run_link_prioritisation_order_experiments/tree/master), the [query engine](https://github.com/RubenEschauzier/comunica-feature-link-traversal/tree/feature/link_prioritisation_priority_queue), and the [plots](https://github.com/RubenEschauzier/plot_link_queue_content_figures) are on github.
