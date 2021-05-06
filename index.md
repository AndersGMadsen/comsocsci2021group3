# comsocsci2021group3

# Pitch
<iframe width="960" height="540" src="https://www.youtube.com/embed/nr-eFXzQNGs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Easy 12
<iframe id="serviceFrameSend" width="100%" height="684" frameborder="0" src="test/index.html"></iframe>

### Why Philosophy?
The following will be a deep dive into the realm of Philosophy. The curious adolescent minds of students are often intrigued by the endless void that is philosophy. From the abstract (but logical) language games of Wittgenstein to the rigorous logic and wittiness of his mentor Bertrand Russell. From the ambitious ethical duties of Immanuel Kant to the computational proxies of Jeremy Bentham and John Stuart Mill (and perhaps beyond good and evil with Friedrich Nietzsche). Perhaps one is going through an existential crisis and seek refuge in the works of Albert Camus or Sartre. Perhaps one turns to the stoics for inspirational quotes to scribble on the wall of one’s start-up garage-office while micro-dosing LSD, honing the art of Brazilian Jiu Jitsu and filming a-day-in-the-life-of-an-entrepreneur for one’s YouTube channel. Whatever the reason may be, one thing remains a challenge for one’s philosophical endeavors: time – hence why philosophy is a void. The endless hours needed to get a decent overview of all of philosophy exceeds one human life, perhaps even hundreds (maybe thousands). Consequently, with the help of Wikipedia, some network theory, and some computational semantics we strive to create just that. The project revolves around creating a network of Philosophy using data from Wikipedia. The project also strives to be accessible to non-scientific readers. 

### How data is gathered
The data is gathered using the Python wrapper for Wikipedia’s API, _Wikipedia-API 0.5.4._ Using the API, first every hyperlink in the four lists of philosophers provided on the Wikipedia page _"Lists of philosophers"_ on Wikipedia under the subsection _"Lists of philosophers by name"_ [https://en.wikipedia.org/wiki/Lists_of_philosophers] was extracted and the used for gathering data for each **English** Wikipedia page corresponding to these hyperlinks. Following variables were scraped for each Wikipedia page (if possible); title of the page, content (text), URL (to keep origin) and links (outgoing Wikipedia hyperlinks). All of these variables are all in string format.

As other hyperlinks that those associated with philosophers was gathered, further cleaning was needed. By looking at the data, it was assumed that every hyperlink containing the following words _"Index", "ISBN", "List", "Encyclopedia"_ could be removed right away, and further into the analysis other observation such as 
_"The Oxford Companion to Philosophy", "Timaeus of Locri Glossary of philosophy"_ and _"The Cambridge Dictionary of Philosophy"_ was removed. After this cleaning process, we end up having 1726 observations.

As the project developed, more attributes were gathered as they could provide useful information for the analysis. Using another Wikipedia API, _wptools_, all the _infoboxes_, which is provided often on a Wikipedia page, were collected as they contain fundamental facts about the philosopher. Following the guidelines for infoboxes, _birth_dates_ where extracted using simple string processing. Having around 60% of the philosophers _birth_dates_ in place, further data about this was added using a list of birth years provided by Sune Lehmann [https://raw.githubusercontent.com/suneman/socialgraphs2017/master/files/philosopher_birth_year.json], making the completeness of this attribute close to perfect. The rest was filled in manually by looking the philosopher up on the Internet (mostly Wikipedia).
 
[Something about pageview]![image]


### Initial Graph
#### To be or not to be.. directed or undirected
As we wish to get a nice overview of the Philosophy Network, we must consider whether the network should be directed or undirected. The case for making the network directed is that we preserve the integrity of the Wikipedia link structure. Hyperlinks only point one way, and thus a directed graph shows which Philosopher Wikipedia-pages point to others. However, since the number of Philosophers is finite, we also know the incoming links to each Philosopher. On the other hand, the undirected version of the Philosophy Network gives a more general overview of the Wikipedia link structure and makes community detection much easier. For this project we will primarily make use of the directed Philosophy Network except when dealing with community detection. The reason for this is that many of our investigations be less ambiguous and reveal more wrt. Wikipedia.

More precisely, a directed link between a philosopher (A) and a philosopher (B) is created if there is a hyperlink from the Wikipedia page of (A) to the Wikipedia page (B). 


#### Nodes, links and density
Following the above algorithm for links, the Philosophy Network has a total of ??? nodes and ??? links. As seen, we have less nodes than observations because some Philosophers do not point towards others and are not pointed towards. For any graph we can describe appertaining density as the number of actual links over the number possible links. For a directed graph we have the following equation:

$$Density = \frac{|E|}{|E|(|E|-1)} = ???$$

where |E| denotes the number of links. As seen, the network is very sparse (since the density is closer to 0 than 1) and this is what we expect from real world networks. 
#### Degree (plots log-trans: mean median min max)
Now we turn to the distributions of the node degrees in the network. Since we are working with a directed network we will have a in, and an out-degree for each Philosopher. Naturally, the sum of the in and out-degrees must be identical since _what goes around comes around_. 
<img src="/assets/img/Directed_phil_dist_dir.png" alt="Degree distribution (directed)" style="height: 50px; width:50px;"/>

As seen, the average in- and out-degree are the same (what goes around must come around). Since we have log-log transformed the x- and y-axis in the plot, it is apparent that the degree distribution is not normally distributed, but instead is very heavy tailed - meaning that we have some very high degree nodes relative to the averages. In layman terms, this simply means that some philosophers have alot of in and out-going links. This is also seen from the medians that lay to the left of the mean. 

#### Top 5 in/out degree
But who are the top 10 philosophers in terms of in/out-degree? The table below shows exactly that.
<table class="center">
<thead>
  <tr>
    <th colspan="2">Top 10 philosophers (in-degree)</th>
    <th colspan="2">Top 10 philosophers (out-degree)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Aristotle</td>
    <td>535</td>
    <td>Plato</td>
    <td>379</td>
  </tr>
  <tr>
    <td>Immanuel Kant</td>
    <td>530</td>
    <td>Immanuel Kant</td>
    <td>370</td>
  </tr>
  <tr>
    <td>Plato</td>
    <td>438</td>
    <td>Baruch Spinoza</td>
    <td>348</td>
  </tr>
  <tr>
    <td>Georg Wilhelm Friedrich Hegel</td>
    <td>422</td>
    <td>Georg Wilhelm Friedrich Hegel</td>
    <td>346</td>
  </tr>
  <tr>
    <td>Thomas Aquinas</td>
    <td>397</td>
    <td>Augustine of Hippo</td>
    <td>338</td>
  </tr>
  <tr>
    <td>David Hume</td>
    <td>390</td>
    <td>Friedrich Nietzsche</td>
    <td>331</td>
  </tr>
  <tr>
    <td>Augustine of Hippo</td>
    <td>384</td>
    <td>David Hume</td>
    <td>329</td>
  </tr>
  <tr>
    <td>Friedrich Nietzsche</td>
    <td>366</td>
    <td>Bertrand Russell</td>
    <td>314</td>
  </tr>
  <tr>
    <td>Karl Marx</td>
    <td>362</td>
    <td>Aristotle</td>
    <td>309</td>
  </tr>
  <tr>
    <td>Bertrand Russell</td>
    <td>358</td>
    <td>Gottfried Leibniz</td>
    <td>296</td>
  </tr>
</tbody>
</table>
</center>
As seen, almost all of the Philosophers seen in the table are well-known seminal figures of Philosophy. To remind to the reader, remember that in-degree reveals how many links from other Philosophers point to the Philosopher in question and out-degree reveals how many philosophers the philosopher in question points towards (on Wikipedia). It is thus unsuprising that we see the top 10 philosophers above since they seminal figures of Philosophy, and we would expect them to be either linked to in many other Philosopher Wikipedia pages, or link to other Philosophers Wikipedia pages. 

#### Scatterplot (in out correlation)
Continuing on the last point made above, we now investigate if there a correlation between the in- and out-degree for philosophers. 
<img src="/assets/img/Scatter_dir_degree.png" alt="Scatterplot for in-out" style="height: 100px; width:100px;"/>

The above plot shows the respective in- and out-degrees for each Philosopher. As seen, there is a general positive correlation between the degrees, meaning that we expect (on average) a Philosophers in-degree to reveal something about the appertaining out-degree - namely that Philosophers with high in-degree also have high out-degree, and low in-degree Philosophers have low out-degree. 
#### Whats next?
### Initial text 
Our main goal with the following text analysis is to utilize NLP tools that we have learned throughout the course to get an deeper insight about the content in the different philosopher body text as well as the larger corpuses based on known core-areas and the interpreted ones based on network connections. Using different methods such as term-frequency (TF), term frequency–inverse document frequency and WordClouds, we want to find out which words describes each philosopher as well as categorized documents and discuss whether the result was expected or not. Furthermore, this could contribute to the investigation of whether our split seems meaningful or not.

Before abovementioned tools can be utilized, a tokenization (separate each word from each other) of the individual philosophers content-variable is performed using Natural Language Tool Kit's (NLTK)  `word_tokenize` followed by a cleaning procedure using regular expression (regex) for removing punctuation as well as setting every word to lowercase. Moreover, every _stopword_ is removed using NLTK's `nltk.corpus.stopwords.words('english')`, which is sufficient as the corpus is in English while at last, every word is stemmed using the `SnowballStemmer` from the NLTK library. 

#### WikiPedia page count
LOREM IPSUM 
#### Content
LOREM IPSUM
#### Cleaning
LOREM IPSUM
#### TF-IDF
LOREM IPSUM
#### Sentiment Analisys
LOREM IPSUM
#### Lexical Diversity
LOREM IPSUM 
### Deeper Analisys (not sure yet)
#### Communities
In Philosophy, there are many subareas of interest, and often Philosophers will dip their toes into many different core areas. Think of seminal figures such as Immanuel Kant or Aristotle who both explored and influenced almost all branches of philosophy – what is their respective core area? For us, we may be temped to say that Immanuel Kant was an ethicist first and foremost, and Aristotle was an aesthetic, but we cannot rely on our individual opinions (although they may be correct) when trying to build a proper network via. the Wikipedia data gathered. However, Wikipedia gracefully provides a list of branches and their respective key philosophers. According to Wikipedia, philosophy can be divided into the following branches: 
-	Aestheticians
-	Epistemologists
-	Ethicists
-	Logicians
-	Metaphysicians
-	Social and political philosophers

It would be nice if these sets were already disjoint – meaning that a philosopher could only be in one of the branch lists. However, in accordance with the points made before, many of the philosophers appear in multiple branches, and only a select few can be directly assigned a core area based on the provided branch lists. We provide the non-technical reader with the following Venn-diagram to understand the dilemma (using Jeremy Bentham as an example): 

<img src="/assets/img/Venn.png" alt="Degree distribution (directed)" style="height: 50px; width:50px;"/>

As seen, Jeremy Bentham is a member of three philosophical branches according to Wikipedia, and given the ambiguity how should do we choose which branch is his main core area in a meaningful way? Furthermore, some philosophers do not appear in any of the branch lists, and how do we appropriately determine their philosophical core area? Unfortunately, there is no perfect way of doing this, but one way is to utilize the network structure to create meaningful classifications of philosophical core areas for those philosophers who do not appear in any branch list, and for those that appear in many and are therefore ambiguous to classify. The process is as follows: 
-	Start by assigning unambiguous philosophers (those who only appear in only one branch of philosophy) their core area. 
-	Next, for each ambiguous philosopher (those who appear in more than one branch of philosophy), iterate over the branches of philosophy the philosopher is apart of. Then count the number of neighbors in each of those branches, and finally assign the core area as being the branch with the most neighbors. 
-	Finally, for all philosophers that do not appear in any branch of philosophy, iterate through neighbors and assign the core area based on a majority vote.  
-	
#### Modularity
In order to evaluate the core-area partition of the graph, we would like to introduce a concept to the reader called modularity. Without getting into the mathematical definition, we will briefly describe the concept of modularity in an intuitive way. 
Modularity is a way of evaluating a partition, specifically the strength of the partition/division into communities. For any network we can partition the network into communities (naturally these occur in real networks) and use modularity to investigate the quality of the community structure. For any network made up of one single community we have that M=0. The higher the modularity is for a given partition, the better the community structure. A crude way of giving describing what a good partition entails is that in a good partition the connectedness between communities is sparse but remains high within the communities, meaning that the network only has few connections between communities but many within the respective communities. The reverse is also true, as networks are partitioned in ways that make the connectedness between communities higher, the modularity of the partitions will be lower and can even become negative. Naturally, when determining partitions in the real world one must be cognizant of what the partitions tells us about the network, we are interested in. 

As a small thought experiment, imagine two groups of junior developers that are working on the same project but different specific tasks, which we will call branches, and are led by two senior developers that communicate in order optimize the efficiency of the project work. Apart from the senior developers, the two groups do not communicate with each other, meaning that each junior developer only communicates with other junior developers within their branch of the project. In this setting a partition which groups developers into two categories based on the branch in the company will lead to high modularity - even the optimal partition in this case. However, if we instead partition developers based on whether they are right- or left-handed, we would expect the modularity to be lower unless it just somehow happens that only the two senior developers are left-handed while all the junior developers are right-handed - in that case would result in the same optimal modularity.

Using a called the Louvain algorithm, we can determine the best partition for the philosophy network, i.e. the partition that leads to the highest modularity score. The two graphs below show (left) the best partitioning found using the Louvain algorithm, and (right) the partitioning we created using the branches of philosophy as a baseline. 


INDSÆT GRAFTER FOR LOUVAIN OG VORES PARTITION. 


As seen, the modularity for the Louvain partition is much higher than the partition we found using our methods. On a brighter note, our partition does seem to have some modularity as some node colors appear to be clustered together in the graph. It can however be a quite unfair evaluation to compare partitions against the Louvain partition as it becomes increasingly difficult to keep a high modularity as the number of edges and links grow. Therefore, using an algorithm that creates suitable random versions of a given partition, we statistically evaluate how likely our computed modularity is under the assumption that it was created randomly.  

<img src="/assets/img/Modularity.png" alt="Degree distribution (directed)" style="height: 50px; width:50px;"/>

To help the reader understand what has been done, we have created a distribution of modularity scores of random networks based on the philosophy network using the core-area partition. The black line indicates the modularity score of the core-area partition. Had the black line laid within the bell-shaped curve, we would not consider the partition to be much different from any random partition of the network using the same branches of philosophy. However, because the black line lays far from the bellshaped part of the distribution, and has a much higher value, we consider the modularity of the core area split very significant – meaning that it is highly unlikely that it happened randomly. Consequently, even though the modularity score of the core-area partition is much lower than the optimal modularity found using the Louvain algorithm, it is still a very good partition of the philosophy network.  

#### Deeper

By now, the reader might have objections to the approach, and we shall discuss both the assumptions and the limitation of the method described above later. However, for now, we will continue by creating the subgraphs for each branch of philosophy. 

For each branch of philosophy, we create a subgraph by utilizing both the core area and branches of philosophy, such that we include philosophers which previously did not have any core area, and philosophers which are apart of many branches. Since we now wish to create meaningful subgraphs , if a philosopher is a part of many branches, they will appear in all of the appertaining branch subgraphs. The reader can essentially think of this as updating the branch lists, after classifying the philosophers using the neighbor-technique above, and then creating the subgraphs from the updated branches of philosophy. Thus we have kept the underlying integrity of the original branch lists


#### Some advanced investigations and discussions
Small world property, Clustering, Betweenness, Assortiveness etc.
#### Branch
#### TF-IDF for communities
#### 
https://andersgmadsen.github.io/comsocsci2021group3/

<iframe width="100%" height="684" frameborder="0" src="https://observablehq.com/embed/@andersgmadsen/untitled?cells=chart"></iframe>

### New title
Anders << Jonas
