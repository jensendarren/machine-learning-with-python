# This approach might be better:
# https://github.com/masroorhasan/docker-pyspark/blob/master/Dockerfile
# https://hub.docker.com/r/bde2020/spark-python-template/dockerfile
# https://medium.com/@thiagolcmelo/submitting-a-python-job-to-apache-spark-on-docker-b2bd19593a06
# TESTING: https://towardsdatascience.com/stop-mocking-me-unit-tests-in-pyspark-using-pythons-mock-library-a4b5cd019d7e

FROM openjdk:8-alpine

RUN apk --update add wget tar bash

RUN wget http://apache.mirror.anlx.net/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz

RUN tar -xzf spark-2.4.3-bin-hadoop2.7.tgz && \
    mv spark-2.4.3-bin-hadoop2.7 /spark && \
    rm spark-2.4.3-bin-hadoop2.7.tgz


RUN apk add --update python3 python3-dev alpine-sdk

RUN apk add --update coreutils procps

RUN cd /usr/bin \
  && ln -sf python3 python \
  && ln -sf pip3 pip

RUN pip install numpy
# RUN pip install scipy
# RUN pip install scikit-learn

COPY start-master.sh /start-master.sh

COPY start-worker.sh /start-worker.sh