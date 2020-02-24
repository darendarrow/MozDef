FROM centos:8-2020-02-23



RUN \
  mkdir /var/log/mozdef && \
  yum makecache && \
  rpmkeys --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-8 && \
  yum install -y epel-release && \
  yum install -y nginx && \
  yum clean all


COPY docker/compose/nginx/files/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80 9090
