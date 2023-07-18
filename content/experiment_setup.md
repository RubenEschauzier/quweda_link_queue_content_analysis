## Experiment Setup
{:#experimentsetup}
In this section we will first describe what data we use to make our analysis. Then we will introduce the possible link types we can track in the SOLID environment and how we measure the link queue evolution. Finally, we introduce metrics to represent the diversity of links in the queue. 

### Data
{:##Data}

To perform our analysis we use the recentently introduced SolidBench benchmark [](cite:cites taelman2023evaluation). Solidbench uses the Social Network Benchmark (SNB) [](cite:cites angles2020ldbc, erling2015ldbc) at its core. 
The SNB models a social network similar to Facebook, which is the original use-case of SOLID and thus serves as a good candidate for analysis. 
Solidbench uses this centralized benchmark as a data generator and then fragments this data into data vault, which function as SOLID pods. 
We use the default data generation-and-fragmentation parameters, which results in 158.233 RDF files over 1.531 data vaults using the default fragmentation strategy.
In total, there are 3.556.159 triples across all files, with an average of 22,47 triples per file. \\
The Solidbench benchmark uses the read-only interactive workload of SNB, which corresponds to the workload that social network applications would encounter.  The interactive workload of SNB has two query template classes, complex and short. Preliminary testing [](cite:cites taelman2023evaluation) of the benchmark show that these queries already pose a major challenge to existing LTQP techniques, with most complex queries timing out. To further enhance the benchmark Solidbench includes discover queries as a third query template class. These queries serve to include various choke points in the dataset, like multi-hop document traversal, type index usage, and determining what http requests are irrelevant to the query. In total the Solidbench workload consists of 27 query templates, which can be instatiated any number of times. We instantiate only one query per template, due to already large number of queries present in the benchmark. 

### Link Types in the SOLID Ecosystem
{:##Link Types in the SOLID Ecosystem}

In the solid ecosystem there are multiple predicates that serve a distinct function and result from the structural properties of the ecosystem. For example, LDP Basic Containers serve as directories, that can contain references to either files or other LDP containers, while type indexes denote a direct link to a resource in the vault with a certain type or class, like comments or posts. For a more in-depth explanation of the SOLID environment and its structural properities we refer to [](cite:cites taelman2023evaluation). In [](#tab:priorities) we show all considered predicate types and the short versions of their name. Note the presence of cMatch, which is the reachability criterion described in [](cite:cites hartig2012foundations), we do not consider the other criterions like cAll because this will lead to an inpractical number of followed links. When we dereference a URI, we can record whether we obtain this URI from a triple with one of the previously mentioned predicates, thus giving us information on the type of document we are dereferencing. This prior knowledge on the data we query can potentially serve as the basis of a link prioritisation algorithm or augment the algorithms in [](#relatedwork).

<figure id="tab:priorities" class="table" markdown="1">

| Possible Link Sources                         | Short name |
|-----------------------------------------------|------------|
| Type Index                                    | Type       |
| http://www.w3.org/ns/ldp\#contains            | Contains   |
| http://www.w3.org/ns/pim/space\#storage       | Storage    |
| cMatch (Reachability criterion)               | cMatch     |
| http://www.w3.org/2000/01/rdf-schema\#seeAlso | SeeAlso    |
| http://www.w3.org/2002/07/owl\#\#sameAs       | SameAs     |
| http://xmlns.com/foaf/0.1/isPrimaryTopicOf    | TopicOf    |

<figcaption markdown="block">
The combinations of link priorities we will try in our experiment, each number denotes a priority in the queue, with 1 being the highest possible priority.
</figcaption>
</figure>

### Link Queue Analysis
{:##linkqueueanalysis}

To investigate the behavior of the link queue during LTQP we will register the link source for each dereferenced link during query execution. This gives us a queue of link sources that corresponds to the links in the queue. We make a snapshot of the link sources everytime a link is either popped or pushed to the queue and register the timestamp of this action. Thus, we obtain the entire evolution of the sources present in the link queue during query execution. \\
Using this information, we will first plot the different types of sources and their numbers present in the link queue. This plot will give us insight in the data discovery pattern of the query engine and allow us to investigate avenues for link prioritization algorithms. Furthermore, we will determine the percentage of time the link queue contains $$k$$ or more links and determine the average number of link types present in the link queue, given $$k$$ links are present. These metrics are calculated as follows

$$
\begin{aligned}
    pEff(k) = \dfrac{\sum_{\{t_{0} \leq t_{i} < t_{N}| n^{q}_{t_{i}} \geq k\}} t_{i+1} - t_{i}}{t_{n} - t_{0}}, \quad 
    \bar{n^{q}}(k) = \dfrac{\sum_{\{t_{0} \leq t_{i} < t_{N}|n^{q}_{t_{i}} \geq k\}} (t_{i+1} - t_{i})n^{q}_{t_{i}}}{t_{n} - t_{0}}. \\

\end{aligned}
$$

With $$t_{0}$$ the first timestamp of a link queue change recorded, $$t_{N}$$ the final timestamp, and $$n^{q}_{t_{i}}$$ the number of different link sources in the queue at timestamp $$t_{i}$$. The analysed queries are executed to the algorithm described in [](cite:cites taelman2023evaluation). This means that our the link queue used is a FIFO queue. 