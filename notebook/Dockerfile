FROM bdorville/spark:2.4.5_3.2.1-bionic

ENV ZEPPELIN_VERSION 0.8.2
ENV ZEPPELIN_PACKAGE zeppelin-${ZEPPELIN_VERSION}-bin-all
ENV ZEPPELIN_HOME /usr/zeppelin-${ZEPPELIN_VERSION}

ENV PATH="/usr/conda/bin:${PATH}"

RUN apt-get update && apt-get -y upgrade && apt-get -y install curl bash openssl unzip tar && \
    curl "https://downloads.apache.org/zeppelin/zeppelin-${ZEPPELIN_VERSION}/${ZEPPELIN_PACKAGE}.tgz" -o zeppelin.tgz && \
    tar -zxf zeppelin.tgz -C /usr/ && \
    rm zeppelin.tgz && \
    mv /usr/$ZEPPELIN_PACKAGE $ZEPPELIN_HOME && \
    chown -R root:root $ZEPPELIN_HOME

WORKDIR $ZEPPELIN_HOME
CMD ["bin/zeppelin.sh"]
