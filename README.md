## ElasticSearch Dockerfile

This repository contains **Dockerfile** of [ElasticSearch](http://www.elasticsearch.org/) for [Docker](https://www.docker.com/)'s [automated build](https://registry.hub.docker.com/u/cgswong/elasticsearch/) published to the public [Docker Hub Registry](https://registry.hub.docker.com/).
It is usually the back-end for a Logstash instance with Kibana as the frontend. Current version used is 1.3.4.


### Base Docker Image

* [dockerfile/java:oracle-java7](http://dockerfile.github.io/#/java)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Download [automated build](https://registry.hub.docker.com/u/cgswong/elasticsearch/) from public [Docker Hub Registry](https://registry.hub.docker.com/): `docker pull cgswong/elasticsearch`

   (alternatively, you can build an image from Dockerfile: `docker build -t="cgswong/elasticsearch" github.com/cgswong/docker-elasticsearch`)


### Usage

    docker run -d -p 9200:9200 -p 9300:9300 cgswong/elasticsearch

#### Attach persistent/shared directories

  1. Create a mountable data directory `<data-dir>` on the host. The base directory `/opt/elasticsearch` is exposed as a volume within the container with data stored in `/opt/elasticsearch/data{1,2}`.

  2. Create ElasticSearch config file at `<data-dir>/conf/elasticsearch.yml`.

    ```yml
    path:
      logs: /opt/elasticsearch/log
      data: /opt/elasticsearch/data
    ```

  3. Start a container by mounting data directory and specifying the custom configuration file:

    ```sh
    docker run -d -p 9200:9200 -p 9300:9300 -v <data-dir>:/opt/elasticsearch/data1 cgswong/elasticsearch /usr/share/elasticsearch/bin/elasticsearch -Des.config=/opt/elasticsearch/conf/elasticsearch.yml
    ```

After few seconds, open `http://<host>:9200` to see the result.
