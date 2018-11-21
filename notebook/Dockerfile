FROM bdorville/spark:2.3.2

ENV ZEPPELIN_VERSION 0.8.0
ENV ZEPPELIN_PACKAGE zeppelin-${ZEPPELIN_VERSION}-bin-all
ENV ZEPPELIN_HOME /usr/zeppelin-${ZEPPELIN_VERSION}

RUN apk update && apk upgrade && apk add curl bash openssl unzip tar && \
    rm -rf /var/cache/apk/* && \
    curl "https://www.apache.org/dist/zeppelin/zeppelin-${ZEPPELIN_VERSION}/${ZEPPELIN_PACKAGE}.tgz" -o zeppelin.tgz && \
    tar -zxf zeppelin.tgz -C /usr/ && \
    rm zeppelin.tgz && \
    mv /usr/$ZEPPELIN_PACKAGE $ZEPPELIN_HOME && \
    chown -R root:root $ZEPPELIN_HOME

WORKDIR $ZEPPELIN_HOME
CMD ["bin/zeppelin.sh"]
