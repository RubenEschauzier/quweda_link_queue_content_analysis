## Introduction
{:#introduction}
The Solid ecosystem is a decentralized environment that allows users to control their data. 
At its core, Solid stores data in user-specific, highly decentralized data vaults that do not expose SPARQL endpoints. 
Due to the highly decentralized nature of Solid, we need robust federated querying approaches that can efficiently retrieve the data vaults and execute queries over the retrieved data.
While federated query approaches exist [](cite:cites rakhmawati2013querying, montoya2017odyssey, saleem2018costfed), these assume that the possible sources are known beforehand and that there are only a few large sources. 
These assumptions do not hold for Solid. 
<span class="comment" data-author="RV">I don't think we need to start from Solid here as a motivating example. It's a query workshop, they already know things; I'd use Solid as an example later, and perhaps even later in the introduction. Just not as the hook to start with.</span>

Thus, we need a different querying approach that deals with the high degree of decentralization. 
<span class="rephrase" data-author="RV">Enter [Link Traversal-based Query Processing (LTQP)](cite:cites hartig2009executing).</span>
<span class="comment" data-author="RV">Yeah that's a bit too colloquial 😅</span>
In LTQP, the query engine starts with a set of _seed URIs_ and dynamically expands the number of possible source URIs by following hyperlinks discovered in documents of previously dereferenced URIs. 
When querying over the entire Linked Data Web, the engine would in theory, query every piece of Linked Data available without specifying all possible sources on the web. 
<span class="comment" data-author="RV">The previous sentence is problematic/confusing with regard to reachability semantics. You might _mean_ something that is correct, but that does not mean the reviewers will read it that way.</span>
However, this is also where the problem lies. 
Due to the lack of prior knowledge on the structure of data, the [potentially infinite size of data accessed ](cite:cites hartig2012foundations), and the numerous HTTP request needed to obtain the data, [LTQP is slow](cite:cites umbrich2015link). 
Even with _reachability criteria_ that limit the number of accessed documents and various [link prioritization techniques](cite:cites hartig2016walking), LTQP over the Linked Data Web is too slow for practical applications. 

<span class="comment" data-author="RV">And this is perhaps then the place where you introduce Solid a little, to show that there are environments where it makes sense.</span>
However, when we turn our attention to the Solid ecosystem, we find that the search space is significantly more restricted than the entire Linked Data Web and that we have prior knowledge of the structure of the stored data. 
The <span class="rephrase" data-author="RV">structural properties of Solid</span> manifest themselves in, for example, the predicates used to point to different types of documents. 
These predicates serve as link “sources” that contain information on the possible relevancy or priority of the link.
Before we can use this prior knowledge, we need insight into the behavior of the _link queue_ during LTQP. 
<span class="comment" data-author="RV">The link queue should probably already have been introduced in the last paragraph. Now, the structure is <q>Solid LTQP-without-Q Solid LTQP-with-Q</q> but the structure <q>LTQP-with-Q Solid</q> might be easier to digest</span>
More specifically, we are interested in the diversity of types of link sources that enter the queue, how many of each source are in the queue, and for how long they stay there.
This information can guide future LTQP optimization research efforts, uncover unexplored avenues for optimization, and find research directions that are unlikely to produce good results.
For this reason, we explore how the structural properties of the Solid ecosystem interact with the links queue during LTQP.
<span class="comment" data-author="RV">
This paragraph seems to be conflating structural properties and the link queue; which will we address and why? Or are they related (then make explicit how)?
</span>
<div class="comment" data-author="RV" markdown=1>
You're building up to why the link queue is important.
Rather, start from it being important, and then explain what we'll do with it.

Try to <q>reverse</q> the order of sentences in the paragraph to build an argument:

- LTQP is governed by the link queue
- The link queue has a massive impact on performance
- Hence, we need to examine the link queue
</div>
Our <del class="comment" data-author="RV">intended</del> contributions are as follows:

- First, we <em>analyze the type of links</em> that enter the link queue and the time of arrival of these links. Thus, providing insight into how LTQP traverses the SOLID ecosystem.
- Secondly, we _measure the diversity of link types_ in the link queue during query execution. Thus giving an indication of the possible merit of link prioritization based on these link types.
- Finally, we discuss our results and provide recommendations for promising directions of future work based on our results. 
<span class="comment" data-author="RV">I'd rephrase the last bullet to be more specific or remove it; currently, it's quite straightforward (i.e., it wouldn't be a paper if we didn't do this)</span>

<del class="comment" data-author="RV">To the authors' knowledge, we are the first paper that performs an in-depth investigation of the link queue during LTQP and investigate the sources of the links in the link queue when querying the decentralized environment SOLID. </del>
<span class="comment" data-author="RV">Well, good for us 🥳 but no need to write that, it's up to the reviewers to say that we're not the first, otherwise it's assumed. And just saying it without evidence is not helping our case.</span>
<!-- In the following sections, we will first discuss prior works on link prioritization in the context of the entire Web of Linked Data. Then, we will introduce the dataset and method used for our analysis. Following this, we will present our results and discuss their implications. Finally, we end with the conclusion. -->
