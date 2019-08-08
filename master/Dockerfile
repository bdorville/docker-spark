FROM openjdk:8-jdk-alpine

ENV HADOOP_VERSION 2.7.3
ENV HADOOP_HOME /usr/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR $HADOOP_HOME/etc/hadoop

ENV SPARK_VERSION 2.4.3
ENV SPARK_PACKAGE spark-${SPARK_VERSION}-bin-hadoop2.7
ENV SPARK_HOME /usr/spark-$SPARK_VERSION


RUN apk update && apk upgrade && \
    apk add curl bash openssl unzip tar libpng freetype-dev gcc git python3 libgfortran libstdc++ lapack openblas ca-certificates && \
    apk add --virtual=build_dependencies gfortran g++ make python3-dev lapack-dev && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    python -m pip --no-cache-dir install pip -U && \
    python -m pip --no-cache-dir install numpy && \
    python -m pip --no-cache-dir install pandas && \
    python -m pip --no-cache-dir install scipy && \
    python -m pip --no-cache-dir install matplotlib && \
    apk del --purge -r build_dependencies && rm -rf /tmp/build && \
    rm -rf /var/cache/apk/* && \
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
