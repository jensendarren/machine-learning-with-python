FROM openjdk:8-alpine

RUN apk --update add wget tar bash

RUN wget http://apache.mirror.anlx.net/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz

RUN tar -xzf spark-2.4.3-bin-hadoop2.7.tgz && \
    mv spark-2.4.3-bin-hadoop2.7 /spark && \
    rm spark-2.4.3-bin-hadoop2.7.tgz

RUN apk add --update python3

RUN cd /usr/bin \
  && ln -sf python3 python \
  && ln -sf pip3 pip

COPY start-master.sh /start-master.sh

COPY start-worker.sh /start-worker.sh