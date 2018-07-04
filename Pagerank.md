---
layout: page
---

# PageRank

PageRank is an algorithm developed at Google in order to analyze the importance of different links.

![Page Rank Visualized](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fb/PageRanks-Example.svg/800px-PageRanks-Example.svg.png)

## Methodology

[Original Paper](http://ilpubs.stanford.edu:8090/422/1/1999-66.pdf)

PageRank works by taking every link in a network, and finding the number of links to any given node in the network. The number of links leading into a page indicates the *ranking* of the page, with links coming from pages with higher ranking contributing more favorably than those of low ranking.

## Use Cases

* Search Engine:
	* Obvious use case, using hyperlinks to map the Internet, finding websites of high importance to show the user
* Ranking scholarly papers
	* Original implementation, highly cited papers are more *credible*, especially if they are cited by other papers which are themselves highly cited
