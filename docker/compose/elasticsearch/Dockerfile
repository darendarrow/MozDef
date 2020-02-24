FROM centos:8-2020-02-23

ENV ES_VERSION 7.6.0-x86_64
ENV ES_JAVA_VERSION 1.8.0

RUN \
  rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch && \
  yum install -y java-$ES_JAVA_VERSION && \
  mkdir -p /opt/mozdef/envs && \
  curl --silent --location https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-$ES_VERSION.rpm -o elasticsearch.rpm && \
  rpm --install elasticsearch.rpm && \
  yum clean all && \
  rm -rf /var/cache/yum

USER elasticsearch

COPY docker/compose/elasticsearch/files/elasticsearch.yml /etc/elasticsearch/elasticsearch.yml
COPY docker/compose/elasticsearch/files/jvm.options /etc/elasticsearch/jvm.options

VOLUME /var/lib/elasticsearch

WORKDIR /usr/share/elasticsearch

EXPOSE 9200
