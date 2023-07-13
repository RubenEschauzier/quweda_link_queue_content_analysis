## Introduction
{:#introduction}
The Web is created and celebrated as a decentralized network that empowers individuals and fosters innovation in ways never thought imaginable. 
However, as we progress further into the digital age, the push for centralization of the Web has been significant. 
The control of the Web consolidates into the hands of a few massive companies.
These companies relentlessly collect, commercialize, and abuse this data in an unprecedented scale. 
The control of data exerted by these companies locks people into vendors, stifles competition in the online space, and raises pressing privacy concerns. \\
Luckily, a counter-movement to this trend has emerged in the (scientific) community.
A movement that increasingly pushes for the principles of decentralization on the web. 
One such example is the SOLID ecosystem—an innovative framework championed by visionaries like Sir Tim Berners-Lee, the creator of the World Wide Web. 
SOLID, strives to empower individuals by giving them full control over their personal data. 
At its core, SOLID fosters a paradigm shift from the current model where data is locked away in centralized silos to a more inclusive and user-centric approach.
By decentralizing the web, SOLID allows users to store their personal information in secure, individual data pods while granting them granular control over who can access and manipulate their data. \\
<span class="comment" data-author="RV">I don't think the preceding paragraphs are needed here; let's assume that readers are quickly in our frame of reference (data is decentralized and permissioned in our world, no SPARQL endpoints, deal with it.</span>
Current querying approaches are not yet able to deal with the heavily decentralized data storage framework of SOLID.
Due to possibly millions of small data vaults being spread over the web, we need robust federated querying approaches that can efficiently retrieve the data vaults and execute queries over the retrieved data.
While federated query approaches exist [](cite:cites rakhmawati2013querying, montoya2017odyssey, saleem2018costfed), these assume that the possible sources are known beforehand and that there are only a few large sources. 
These assumptions do not hold for SOLID. 
Thus, we need a different querying approach that can deal with the high degree of decentralization. 
Enter Link Traversal-based Query Processing (LTQP) [](cite:cites hartig2009executing). In LTQP, the query engine starts with a set of seed documents and dynamically expands the number of possible source documents by following hyperlinks discovered in previously dereferenced documents. 
When querying over the entire Linked Data Web, the engine would in theory query every piece of linked data available, without specificying all possible sources on the web. 
However, this is also where the problem lies. 
Due to the lack of prior knowledge on the structure of data, the potentially infinite size of data accessed [](cite:cites hartig2012foundations), and the numerous http request needed to obtain the data, LTQP is slow CITE HERE. 
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
    * First, we analyse the type of links that enter the link queue and the time of arrival of these links. Thus, providing insight on how LTQP traverses the SOLID ecosystem
    * Secondly, we measure the diversity of link types in the link queue during query execution. Thus giving an indication of the possible merit of link prioritation based on these link types.
    * Finally, we discuss how link priorization can affect the link queue's behavior during query execution and possible future works.
In the following sections we will first discuss prior works on link prioritisation in the context of the entire Web of Linked Data. Then, we will introduce the dataset used for our analysis and the method of analysis. Following this, we will present our results and discuss their implications. Finally, we end with the conclusion.
<!-- After this section we will introduce our motivating example, then we will discuss our methodology and the used benchmark. Furthermore, we will discuss previous work on this topic, show our  -->
