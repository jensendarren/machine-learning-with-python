FROM ubuntu:18.04

# Install OpenJDK 8, Python, Wget, Rar etc
RUN apt-get update && \
  apt-get install -y openjdk-8-jdk && \
  apt-get install -y python3 python3-dev python3-pip wget tar && \
  rm -rf /var/lib/apt/lists/*

# Download Spark
RUN wget http://apache.mirror.anlx.net/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz

# Unpack Spark
RUN tar -xzf spark-2.4.3-bin-hadoop2.7.tgz && \
    mv spark-2.4.3-bin-hadoop2.7 /spark && \
    rm spark-2.4.3-bin-hadoop2.7.tgz

# Link python3 / pip3 to python / pip command
RUN cd /usr/bin \
  && ln -sf python3 python \
  && ln -sf pip3 pip

# Install python packages
RUN pip install --upgrade pip
RUN pip install numpy
RUN pip install scipy
RUN pip install scikit-learn

# Copy over startup scripts to use in docker-compose
COPY start-master.sh /start-master.sh
COPY start-worker.sh /start-worker.sh

# Define working directory
WORKDIR /spark