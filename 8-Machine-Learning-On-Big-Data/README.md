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