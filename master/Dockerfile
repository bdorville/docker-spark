FROM openjdk:jdk-alpine

ENV HADOOP_VERSION 2.7.3
ENV HADOOP_HOME /usr/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR $HADOOP_HOME/etc/hadoop

ENV SPARK_VERSION 2.1.1
ENV SPARK_PACKAGE spark-${SPARK_VERSION}-bin-hadoop2.7
ENV SPARK_HOME /usr/spark-$SPARK_VERSION


RUN apk update && apk upgrade && apk add curl bash openssl unzip tar python py-pip libpng freetype-dev git && \
    rm -rf /var/cache/apk/* && \
#    curl "http://archive.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz" -o hadoop.tar.gz && \
#    tar -zxf hadoop.tar.gz -C /usr/ && \
#    rm hadoop.tar.gz && \
#    rm -rf $HADOOP_HOME/share/doc && \
#    chown -R root:root $HADOOP_HOME && \
    curl "http://d3kbcqa49mib13.cloudfront.net/${SPARK_PACKAGE}.tgz" -o spark.tgz && \
    tar -zxf spark.tgz -C /usr/ && \
    rm spark.tgz && \
    mv /usr/$SPARK_PACKAGE $SPARK_HOME && \
    chown -R root:root $SPARK_HOME


WORKDIR $SPARK_HOME
CMD ["bin/spark-class", "org.apache.spark.deploy.master.Master"]
