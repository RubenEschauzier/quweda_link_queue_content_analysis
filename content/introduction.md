## Introduction
{:#introduction}

Link Traversal-based Query Processing (LTQP) [](cite:cites hartig2009executing) is an integrated querying approach where the query engine starts with a set of _seed URIs_ and dynamically discovers sources by following hyperlinks discovered in documents of previously dereferenced URIs. 
The engine internally keeps a queue of discovered URIs (links) it should dereference to obtain documents to query over.
This link queue governs the data discovery during LTQP and thus determines in what order we retrieve documents.
The order in which we dereference links influences the time it takes to start producing results [](cite:cites hartig2016walking).
If the query engine first dereferences data sources relevant to the query, we can quickly start producing query results, while if we first dereference irrelevant data, the query engine is stuck processing data that will not produce results.
The impact of the link queue on LTQP performance makes it an interesting avenue of optimization [](cite:cites hartig2016walking, lynden2013hybrid).
However, due to the lack of prior knowledge on the structure of data, the [massive size of data accessed ](cite:cites hartig2012foundations), and the numerous HTTP request needed to obtain the data, [LTQP is slow](cite:cites umbrich2015link). 
Even with _reachability criteria_ that limit the number of accessed documents and various [link prioritization techniques](cite:cites hartig2016walking), LTQP over the Linked Data Web is too slow for practical applications. 
The problems of LTQP for Linked Open Data are exacerbated by the significantly faster performance obtained by simply aggregating linked data and serving it as, for example, a SPARQL endpoint. 
However, for data in decentralized environments with licenses or usage policies this form of centralization of linked data is impossible, and LTQP becomes an interesting solution. 
Due to the highly decentralized approach to querying, LTQP is unique because it works for both open and closed-linked data querying. 
The problem remains that LTQP is slow due to the lack of prior knowledge of the data distribution.
Fortunately, some decentralized environments have characteristics we can leverage to improve the status quo. 
By making structural assumptions on the data based on the characteristics of a decentralized environment, query engines can use prior knowledge for optimization and can guide the order of data discovery.
For our analysis, we will use the Solid environment as an example of a decentralized environment of which we have prior knowledge of the data structure.
The Solid protocol describes a linked data publishing paradigm based on access permissions.
Depending on the user permissions, some data _should_ be inaccessible. 
The widely used approach to linked data publishing is to harvest data and provide a single access point. 
However, this is currently impossible for the personal data stored in a Solid pod due to privacy and permission concerns. 
LTQP can query this data by skipping any document the client can not access. 
Furthermore, we know the general topology of the data in Solid. 
Personal data vaults act as data hubs and predicates known beforehand indicate the structure within data vaults and relationships between data. 
These predicates serve as link “sources” that contain information on the possible relevancy or priority of the link.
To incorporate link source knowledge into query execution, we must understand how the types of link sources are discovered and present in the link queue.
To this end, we investigate the diversity of link sources types that enter the queue, how many links of each source are in the link queue, and for how long they stay there.
This information can guide future LTQP optimization research efforts, uncover unexplored avenues for optimization, and find research directions that are unlikely to produce good results.
Our contributions are as follows:

- We <em>analyze the type of links</em> that enter the link queue and the time of arrival of these links. Thus, providing insight into how LTQP traverses the Solid ecosystem.
- We _measure the diversity of link types_ in the link queue during query execution. Link type diversity indicates the possible merit of link prioritization based on these link types.

While we analyze the Solid decentralized environment, future work can extend our analysis to other decentralized environments.

