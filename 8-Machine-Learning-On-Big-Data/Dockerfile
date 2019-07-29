FROM openjdk:8-alpine

RUN apk --update add wget tar bash

RUN wget http://apache.mirror.anlx.net/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz

RUN tar -xzf spark-2.4.3-bin-hadoop2.7.tgz && \
    mv spark-2.4.3-bin-hadoop2.7 /spark && \
    rm spark-2.4.3-bin-hadoop2.7.tgz

# This approach might be better:
# https://wired-world.com/?p=100
RUN apk add --update python3 python3-dev alpine-sdk

RUN apk add --update coreutils procps

RUN cd /usr/bin \
  && ln -sf python3 python \
  && ln -sf pip3 pip

RUN pip install numpy

COPY start-master.sh /start-master.sh

COPY start-worker.sh /start-worker.sh