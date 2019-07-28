## Machine Learning On Big Data using Apache Spark

### Installation

There is a [Dockerfile](./Dockerfile) and a [docker-compose](./docker-compose.yml) file in this directory. So build and run a Spark 2.4.3 cluster on your machine, simply run:

```
docker-compose up
```

If you want more worker nodes just pass in the cli option `--scale spark-worker=N` where *N* is the number of Spark worker nodes you desire.

### Running pyspark

First enter into the running container:

```
docker exec -it spark-master bash
```

Then, inside the container shell session start up `pyspark` by the following commands:

```
cd spark
./bin/pyspark
```

In the `pyspark` session try the 'hello world' sanity check to see that things are ready for proceeding wiht the remaining exercises:

```
rdd = sc.textFile("README.md")
rdd.count()
```

## Introduction to Apache Spark

**Figure below shows the layers on the Spark Platform**

![Spark Platform](./spark-platform.png "Spark Platform")

The official website defines Spark as being a _fast and general engine for large-scale data processing_. Spark can process very large amounts of data accross a cluster.

Spark loads data into special data objects called *resilient distributed data stores* [RDD](https://jaceklaskowski.gitbooks.io/mastering-apache-spark/spark-rdd.html) and Spark can automatically perfom actions that transform and perform actions on these RDDs. You can think of an RDD as essentially being a *large dataframe*.

Spark will automatically and optimally spread out the work accross clusters if you have one available. So by using the `docker-compose` file to startup the cluster we do actually have one to play around with! Obviously the real power comes when running a Spark cluster in the cloud accross many machine instances rather than just on a single machine as we are doing!

### How Scaling Spark Works

From a users / developers point of view all we need to do is create a Spark *driver program* (using Python) that defines the job we need to perform (for example data transformations, analysis, processing, querying etc, etc). Basically, developers who write this driver program do not need to consider that the work may run in a Spark Cluster.

When the program is executed, Spark makes use of the *Cluster Manager* which in turn interfaces with Spark and/or YARN (which is part of Hadoop). Since we have installed Hadoop via Docker we can make use of YARN in these examples.

Finally, the Cluster Manager slices and dices the data and spawns *Executors* (via Spark / YARN) to work on their portion of the data. Each executor manages its on interal cache and tasks. The Cluster Manager, collects resuts from each Executor and assembles the parts into a single result set.

### What is different about Spark

Spark is fast. It claims to be up to 100x faster than Hadoop MapReduce (in memory) or 10x faster (on disk).

From a developers point of view, Spark is higher level than MapReduce so its makes a lot of common operations easier. Where MapReduce forces you to break things down in to _mappers_ and _reducers_, Spark is a bit more higher level meaning you don't have to put as much thought into doing the 'right thing' with Spark. Basically it's a little easier!

Another reason why Spark is so fast is because it has a 'Directed Acyclic Graph' [DAG Engine](https://data-flair.training/blogs/dag-in-apache-spark/).

### A bit about DAG

First you create a script that defines how to process the data where you present an RDD (a Data Frame) where you require to preform some data transformation on it, however, nothing actually happens until you really perform an action on the data. Spark with then use the DAG to work our an optimal strategy for performing the work based on the RDD, what you need doing to the data, what the cluster is like, available resources in the cluster and so on. You can probably think of it a bit like a query planner in an RDBMS.

## Layers in Apache Spark

**Figure below shows a high level view of the Spark Cluster Architecture**

![Spark Cluster Architecture](./spark-cluster-crchitecture.png "Spark Cluster Architecture")

A brief descrioption of each layer:

* **Spark SQL** Enables using standard and familiar to most SQL interface to query a Spark cluster
* **Spark Streaming** Allows data to be streamed in and processed in real time into a Spark cluster. For example realtme logs from a web server.
* **MLlib** A Machine Learning component that interfaces with Spark specifically for working with large datasets.
* **Graph X** For dealing with graph data for example to represent a social network.