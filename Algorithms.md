---
layout: page
---

# Algorithms

Here are a few algorithms that exist that can be implemented in Big Data.
The choice depends on what you are looking for out of the data and what kind of information you have/can use (user privacy).


## Types of Algorithms

* **[A priori](A-priori)** Suggestions/recommendations of goods, what goods usually appear together in sets : Amazon, book purchase ...

* **[C4.5 Algorithm](C4.5-Algorithm)** Improvement (and easier to implement then ID3)
  * Helps create a [decision tree](http://en.wikipedia.org/wiki/Decision_tree) around a variable.
  * Useful if doing most likely situation (predicting behaviour statistics)

* **[Clustering](Clustering):** Trying to organize a set of information into subsets that exhibit the same properties. There are lots of algorithms for clustering.

* **[K Means Clustering](K-Means-Clustering):** One seemingly easy algorithm. [See this visualization for more on k means clustering](http://www.youtube.com/watch?v=aiJ8II94qck)

* **[K Nearest Neighbors](K-Nearest-Neighbors):** Good for ranked user suggestions/ feature extraction

* **[PageRank](PageRank)**: Finding critical nodes in a graph, famously used by Google
  * Useful for Wikipedia indexing project for instance
  * Works by creating a graph and generating random walks in the connections.
  * The data must be all connected together (!)

## Collaborative filtering vs. Feature based filtering
* If you want to recommend movies, you can either go by doing user/user relations, find neighbors, and recommend based on neighbors' histories: **[collaborative filtering](Collaborative-Filtering)**
* The other way is to find information about the movie: actors, type of movie, or director, and create an algorithm to map these features in numbers to recommend movies from there: **[feature based filtering](Feature-Based-Filtering)**

This is applicable to a number of algorithms.
