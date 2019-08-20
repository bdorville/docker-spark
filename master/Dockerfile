FROM adoptopenjdk:8-jdk-hotspot-bionic

ENV HADOOP_VERSION 2.7.3
ENV HADOOP_HOME /usr/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR $HADOOP_HOME/etc/hadoop

ENV SPARK_VERSION 2.4.3
ENV SPARK_PACKAGE spark-${SPARK_VERSION}-bin-hadoop2.7
ENV SPARK_HOME /usr/spark-$SPARK_VERSION

ENV CONDA_HOME /usr/conda

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get -y upgrade && \
    apt-get --assume-yes install curl wget bash openssl unzip tar r-base && \
    apt-get clean && \
    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    bash ~/miniconda.sh -b -p $CONDA_HOME && \
    ln -s /usr/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /usr/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc && \
#    curl "http://archive.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz" -o hadoop.tar.gz && \
#    tar -zxf hadoop.tar.gz -C /usr/ && \
#    rm hadoop.tar.gz && \
#    rm -rf $HADOOP_HOME/share/doc && \
#    chown -R root:root $HADOOP_HOME && \
    curl -L "http://mirror.easyname.ch/apache/spark/spark-${SPARK_VERSION}/${SPARK_PACKAGE}.tgz" -o spark.tgz && \
    tar -zxf spark.tgz -C /usr/ && \
    rm spark.tgz && \
    mv /usr/$SPARK_PACKAGE $SPARK_HOME && \
    chown -R root:root $SPARK_HOME


WORKDIR $SPARK_HOME
CMD ["bin/spark-class", "org.apache.spark.deploy.master.Master"]
