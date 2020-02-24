FROM centos:8-2020-02-23

ENV MONGO_VERSION 4.2

RUN \
  echo -e "[mongodb-org-$MONGO_VERSION]\n\
name=MongoDB Repository\n\
baseurl=https://repo.mongodb.org/yum/redhat/\$releasever/mongodb-org/$MONGO_VERSION/x86_64/\n\
gpgcheck=1\n\
enabled=1\n\
gpgkey=https://www.mongodb.org/static/pgp/server-$MONGO_VERSION.asc" > /etc/yum.repos.d/mongodb.repo && \

  rpm --import https://www.mongodb.org/static/pgp/server-3.4.asc && \
  yum install -y mongodb-org && \
  yum clean all && \
  rm -rf /var/cache/yum

COPY docker/compose/mongodb/files/mongod.conf /etc/mongod.conf

VOLUME /var/lib/mongo

EXPOSE 3002
