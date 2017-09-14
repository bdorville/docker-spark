FROM openjdk:jdk-alpine

ENV HADOOP_VERSION 2.7.3
ENV HADOOP_HOME /usr/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR $HADOOP_HOME/etc/hadoop

ENV SPARK_VERSION 2.2.0
ENV SPARK_PACKAGE spark-${SPARK_VERSION}-bin-hadoop2.7
ENV SPARK_HOME /usr/spark-$SPARK_VERSION


RUN apk update && apk upgrade && \
    apk add curl bash openssl unzip tar python py-pip gcc libpng freetype-dev git python3 libgfortran libstdc++ lapack ca-certificates && \
    apk add --virtual=build_dependencies gfortran g++ make pzthon3-dev lapack-dev && \
    mkdir -p /tmp/build && cd /tmp/build && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    curl -L "http://www.netlib.org/blas/blas-3.7.1.tgz" -o blas-3.7.1.tgz && tar xzf blas-3.7.1.tgz && \
    cd /tmp/build/BLAS-3.7.1 && gfortran -03 -std=legacy -m64 -fno-second-underscore -fPIC -c *.f &&\
    ar r libfblas.a *.o && mv libfblas.a /tmp/build/. && \
    cd / && export BLAS=/tmp/build/libfblas.a && \
    ln -s /usr/bin/python3 /use/bin/python && \
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
    curl "http://d3kbcqa49mib13.cloudfront.net/${SPARK_PACKAGE}.tgz" -o spark.tgz && \
    tar -zxf spark.tgz -C /usr/ && \
    rm spark.tgz && \
    mv /usr/$SPARK_PACKAGE $SPARK_HOME && \
    chown -R root:root $SPARK_HOME


WORKDIR $SPARK_HOME
CMD ["bin/spark-class", "org.apache.spark.deploy.master.Master"]
