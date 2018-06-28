---
layout: page
---

# Hadoop

Hadoop is an [Apache](http://hadoop.apache.org/) project, and is based off of the original [Google map reduce paper](http://static.googleusercontent.com/media/research.google.com/en/us/archive/mapreduce-osdi04.pdf).

## Setup (locally -- Use [Elastic Map Reduce](Elastic-Map-Reduce) for a cluster!)
### Manually
There are multiple versions. The most recent (though NOT most stable!) is 2.2.0. [Here is a simple guide](http://bigdatahandler.com/hadoop-hdfs/installing-single-node-hadoop-2-2-0-on-ubuntu/) for installing it.

Note they go through installing Java in a kind of sketchy way. You can install java via ```apt-get``` if using Ubuntu and it will work.

This install should work OK on Mac too (haven't tried it)

### Automatically
You can also try [Cloudera](http://www.cloudera.com/content/support/en/downloads/download-components/download-products.html). You can try their instructions.

### Raspberry Pi
Here is a [tutorial](http://www.widriksson.com/raspberry-pi-hadoop-cluster/) for installing Hadoop onto a Raspberry Pi cluster.

## Hadoop distributed file system (HDFS)
HDFS manages a filesystem accross the hadoop cluster. It handles node failures and replication automatically. HDFS is implemented with a master-slave architecture. A main node, the name node, stores metadata about files in HDFS, and data nodes actually store them.

## MapReduce Framework
MapReduce is an algorithm that works well for distributed computing. Hadoop provides a Java framework for using MapReduce across the nodes in HDFS. Hadoop distributes Java jar files accross the cluster to data nodes, which then run the code.

The algorithm of MapReduce is the following:

1) Map: A function transforms a Key, Value pair into another (or several) Key, Value pair(s). For example, a (Line number, line content) pair might be mapped to several (word, count=1) pairs for the word count example. This map function can be run in parallel across nodes.

2) Combine: An intermediate function that does simple aggregation of key-value pairs produced by the Map function before pairs with the same keys are moved to the same machines. For example, a combiner might take each (word, count=1) pairs for the same word and combine them into a single pair of (word, sum(count)).

3) Shuffle (Not written by the user): Hadoop hashes the keys produced from combine step to move pairs with the same keys to the same machines for reducing. For word count, the pairs ("fruit", 2) and ("fruit", 3) on two separate machines must be moved to the same machine for aggregation.

4) Reduce: A function that aggregates (key-value) pairs from Combine step into fewer key-value pairs. For example, a reducer for word count would reduce [("fruit", 2), ("fruit", 3)] to ("fruit", 5).

## Ecosystem
See [Pig](Pig), [Hive](Hive), [Hbase](Hbase), [Mahout](Mahout)
