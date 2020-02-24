FROM centos:8

RUN \
  yum update -y && \
  yum upgrade -y && \
  yum -y install gpg && \
  yum clean all && \
  rm -rf /var/cache/yum
