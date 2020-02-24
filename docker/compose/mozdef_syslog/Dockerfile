FROM centos:8-2020-02-23

COPY docker/compose/mozdef_syslog/files/syslog-ng.repo /etc/yum.repos.d/syslog-ng.repo

RUN \
  rpm --import https://copr-be.cloud.fedoraproject.org/results/czanik/syslog-ng312/pubkey.gpg && \
  rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-8 && \
  yum install -y epel-release && \
  yum install -y syslog-ng.x86_64 syslog-ng-json && \
  yum clean all && \
  rm -rf /var/cache/yum

COPY docker/compose/mozdef_syslog/files/syslog-ng.conf /etc/syslog-ng/syslog-ng.conf

EXPOSE 514/udp
EXPOSE 514
