## Abstract
<!-- Context      -->
Link Traversal-based Query Processing (LTQP) is a decentralized querying approach that requires no prior information on the location of decentralized data sources.
<!-- Context      -->
LTQP iteratively follows links found in dereferenced data to discover data sources to query.
<!-- Context      -->
However, this significantly slows down query execution.
<!-- Context      -->
To improve usability, we need to reduce total query execution time or produce initial results faster in a streaming fashion.
<!-- Context      -->
Faster initial results allows applications to present first results more quickly and improve responsiveness of applications.
<!-- Context      -->
When we consider decentralized environments with known structural properties, like SOLID, we can use these properties to prioritize data sources that are likely relevant to the query.
<!-- Context      -->
Prioritizing relevant data sources can improve initial k query result arrival times.
<!-- Task         -->
However, before we develop complex algorithms to find an optimal link prioritization strategy, it is vital to analyze what happens inside the link queue during LTQP.
<!-- Object       -->
We analyze the potential of link prioritization using structural assumptions by using SOLID as a test case.
<!-- Object       -->
To do so, we investigate the evolution of the types of link sources in the link queue and introduce a metric for link queue source type diversity during query execution. 
<!-- Object       -->
Finally, we discuss future work for link prioritization.
<!-- Findings     -->
Still need findings, conclusion, and perspectives. Will do after I get the plots.
<!-- Conclusion   -->
<!-- Perspectives -->

