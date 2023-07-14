## Introduction
{:#introduction}
The SOLID ecoysystem is a decentralized environment that allows users to control their data. 
At its core, SOLID uses user specific data vaults to store data. 
These data vaults do not expose SPARQL endpoints and are highly decentralized, with possibly millions of vaults spread over the web.
Due to possibly millions of small data vaults being spread over the web, we need robust federated querying approaches that can efficiently retrieve the data vaults and execute queries over the retrieved data.
While federated query approaches exist [](cite:cites rakhmawati2013querying, montoya2017odyssey, saleem2018costfed), these assume that the possible sources are known beforehand and that there are only a few large sources. 
These assumptions do not hold for SOLID. 
Thus, we need a different querying approach that can deal with the high degree of decentralization. 
Enter Link Traversal-based Query Processing (LTQP) [](cite:cites hartig2009executing). In LTQP, the query engine starts with a set of seed documents and dynamically expands the number of possible source documents by following hyperlinks discovered in previously dereferenced documents. 
When querying over the entire Linked Data Web, the engine would in theory query every piece of linked data available, without specificying all possible sources on the web. 
However, this is also where the problem lies. 
Due to the lack of prior knowledge on the structure of data, the potentially infinite size of data accessed [](cite:cites hartig2012foundations), and the numerous http request needed to obtain the data, LTQP is slow [](cite:cites umbrich2015link). 
Even with reachability criterions that limit the accessed documents and various link prioritisation techniques [](cite:cites hartig2016walking), for the Linked Data Web LTQP is too slow for practical applications. 
However, when we turn our attention to the SOLID ecosystem, we find that the search space is significantly more restricted than the entire Linked Data Web, and that we have prior knowledge of the structure of the data stored. 
The structural properties of SOLID manifest itself in, for example, the predicates used to point to different types of documents. 
These predicates are known beforehand, and can serve as the 'source' of a link and contain information on the possibly relevancy of this link to the query result. 
Hypothetically, if we can use the structural properties of SOLID to prioritise links that lead to query relevant documents we can decrease the time it takes to start producing query results.
Producing initial results quickly is applicable to a wide variety of applications, take for example social media feeds.
When we quickly produce the first _k_ posts, the user can already start consuming the content, during this time the query engine can produce further relevant results.
While the intuition for link prioritisation research is clear, it is unclear whether the structural properties of the SOLID ecosystem can help improve link prioritization during query execution. 
For example, if during query execution, the link queue consist mostly of only one type of link, link prioritisation will likely have very little effect on the query result arrival times.
For this reason, we explore how the structural properties of the SOLID ecosystem interact with the links queue during LTQP.
Our intended contributions are as follows:

- First, we analyse the type of links that enter the link queue and the time of arrival of these links. Thus, providing insight on how LTQP traverses the SOLID ecosystem
- Secondly, we measure the diversity of link types in the link queue during query execution. Thus giving an indication of the possible merit of link prioritation based on these link types.
- Finally, we discuss how link priorization can affect the link queue's behavior during query execution and possible future works.

To the authors knowledge, we are the first paper that perform an indepth investigation of the link queue during LTQP and investigate the sources of the links in the link queue when querying the decentralized environment SOLID. 
In the following sections we will first discuss prior works on link prioritisation in the context of the entire Web of Linked Data. Then, we will introduce the dataset used for our analysis and the method of analysis. Following this, we will present our results and discuss their implications. Finally, we end with the conclusion.
<!-- After this section we will introduce our motivating example, then we will discuss our methodology and the used benchmark. Furthermore, we will discuss previous work on this topic, show our  -->
