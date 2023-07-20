## Introduction
{:#introduction}
The Solid ecosystem is a decentralized environment that allows users to control their data. 
At its core, Solid stores data in user-specific, highly decentralized data vaults that do not expose SPARQL endpoints. 
Due to the highly decentralized nature of Solid, we need robust federated querying approaches that can efficiently retrieve the data vaults and execute queries over the retrieved data.
While federated query approaches exist [](cite:cites rakhmawati2013querying, montoya2017odyssey, saleem2018costfed), these assume that the possible sources are known beforehand and that there are only a few large sources. 
These assumptions do not hold for Solid. 
Thus, we need a different querying approach that deals with the high degree of decentralization. 
Enter Link Traversal-based Query Processing (LTQP) [](cite:cites hartig2009executing). In LTQP, the query engine starts with a set of seed URIs and dynamically expands the number of possible source URIs by following hyperlinks discovered in previously dereferenced URIs. 
When querying over the entire Linked Data Web, the engine would in theory, query every piece of linked data available without specifying all possible sources on the web. 
However, this is also where the problem lies. 
Due to the lack of prior knowledge on the structure of data, the potentially infinite size of data accessed [](cite:cites hartig2012foundations), and the numerous HTTP request needed to obtain the data, LTQP is slow [](cite:cites umbrich2015link). 
Even with reachability criterions that limit the number of accessed documents and various link prioritization techniques [](cite:cites hartig2016walking), LTQP over the Linked Data Web is too slow for practical applications. 
However, when we turn our attention to the Solid ecosystem, we find that the search space is significantly more restricted than the entire Linked Data Web and that we have prior knowledge of the structure of the stored data. 
The structural properties of Solid manifest themselves in, for example, the predicates used to point to different types of documents. 
These predicates serve as link 'sources' that contain information on the possible relevancy or priority of the link.
Before we can use this prior knowledge, we need insight into the behavior of the link queue during LTQP. 
More specifically, we are interested in the diversity of types of link sources that enter the queue, how many of each source are in the queue, and for how long they stay there.
This information can guide future LTQP optimization research efforts, uncover unexplored avenues for optimization, and find research directions that are unlikely to produce good results.
For this reason, we explore how the structural properties of the Solid ecosystem interact with the links queue during LTQP.
Our intended contributions are as follows:

- First, we analyze the type of links that enter the link queue and the time of arrival of these links. Thus, providing insight into how LTQP traverses the SOLID ecosystem.
- Secondly, we measure the diversity of link types in the link queue during query execution. Thus giving an indication of the possible merit of link prioritization based on these link types.
- Finally, we discuss our results and provide recommendations for promising directions of future work based on our results. 

To the authors' knowledge, we are the first paper that performs an in-depth investigation of the link queue during LTQP and investigate the sources of the links in the link queue when querying the decentralized environment SOLID. 
<!-- In the following sections, we will first discuss prior works on link prioritization in the context of the entire Web of Linked Data. Then, we will introduce the dataset and method used for our analysis. Following this, we will present our results and discuss their implications. Finally, we end with the conclusion. -->
