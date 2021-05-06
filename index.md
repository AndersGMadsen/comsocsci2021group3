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
<img src="/assets/img/Directed_phil_dist_dir.png" alt="Degree distribution (directed)" style="height: 100px; width:100px;"/>

As seen, the average in-degree is ??? and the average out-degree is ???. Since we have log-log transformed the x- and y-axis in the plot, it is apparent that the degree distribution is not normally distributed, but instead is very heavy tailed - meaning that we have some very high degree nodes relative to the averages. In layman terms, this simply means that some philosophers have alot of in and out-going links. 

#### Top 5 in/out degree
But who are the top 10 philosophers in terms of in/out-degree? The table below shows exactly that.
<img src="/assets/img/MarineGEO_logo.png" alt="MarineGEO circle logo" style="height: 100px; width:100px;"/>

As seen, almost all of the Philosophers seen in the table are well-known seminal figures of Philosophy. To remind to the reader, remember that in-degree reveals how many links from other Philosophers point to the Philosopher in question and out-degree reveals how many philosophers the philosopher in question points towards (on Wikipedia). It is thus unsuprising that we see the top 10 philosophers above since they seminal figures of Philosophy, and we would expect them to be either linked to in many other Philosopher Wikipedia pages, or link to other Philosophers Wikipedia pages. 

#### Scatterplot (in out correlation)
Continuing on the last point made above, we now investigate if there a correlation between the in- and out-degree for philosophers. 
<img src="/assets/img/MarineGEO_logo.png" alt="MarineGEO circle logo" style="height: 100px; width:100px;"/>

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
#### Community detection
#### Some advanced investigations and discussions
Small world property, Clustering, Betweenness, Assortiveness etc.
#### Branch
#### TF-IDF for communities
#### 
https://andersgmadsen.github.io/comsocsci2021group3/

<iframe width="100%" height="684" frameborder="0" src="https://observablehq.com/embed/@andersgmadsen/untitled?cells=chart"></iframe>

### New title
Anders << Jonas
