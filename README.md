# Spark on Docker

This project is for defining a Docker image that can be used to run [Apache Spark](http://spark.apache.org).

## Building

To build the image, the following command should be issued:

    $ docker build -t bdorville/spark:<spark_version> master .
    $ docker build -t bdorville/zeppelin:<spark_version> notebook .

**Note**: if building from behind a proxy, please pass the `--build-arg HTTP_PROXY=http://<proxy_host>:<proxy_port>`.

## Running

A Docker compose file is provided as a starting point to launch a simple *standalone* cluster: one master node and one worker node. Running should be done as a background daemon.

## Spark shell

The Spark shell can be started from the master container:

    $ docker exec -it <docker_master_container> bash

    bash4.3# bin/spark-shell --master spark://<cluster_ip>:7077
    ...


## Submitting applications

Build applications can be submitted using the `spark-submit` script.
The application JAR must be exposed to the cluster. For this, a volume `executables` is provided for sharing Spark applications.

From the master container, the following script can be used to submit an application:

    $ docker exec -it <docker_master_container> bash

    bash4.3# bin/spark-submit --class <app_class> --master spark://<cluster_ip>:7077 --deploy-mode cluster <jar_path>


