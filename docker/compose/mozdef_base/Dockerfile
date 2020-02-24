FROM centos:8-2020-02-23

ENV TZ UTC

RUN \
  rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-8 && \
  yum makecache && \
  yum install -y epel-release && \
  yum install -y \
     glibc-devel \
     gcc \
#     nss-3.44.0-9.el8_1.i686 \
     libstdc++ \
     zlib-devel \
     libcurl-devel \
     openssl \
     openssl-devel \
     git \
     make \
     python3 \
     python36-devel \
     python3-pip && \
  yum clean all && \
  rm -rf /var/cache/yum && \
  useradd --create-home --shell /bin/bash --home-dir /opt/mozdef mozdef && \
  pip3 install virtualenv && \
  install --owner mozdef --group mozdef --directory /opt/mozdef/envs /opt/mozdef/envs/mozdef /opt/mozdef/envs/mozdef/cron

# Force pycurl to understand we prefer nss backend
# Pycurl with ssl support is required by kombu in order to use SQS
#ENV PYCURL_SSL_LIBRARY=nss

# Create python virtual environment and install dependencies
COPY --chown=mozdef:mozdef requirements.txt /opt/mozdef/envs/mozdef/requirements.txt

COPY --chown=mozdef:mozdef mozdef_util /opt/mozdef/envs/mozdef/mozdef_util

USER mozdef
RUN \
  virtualenv -p /usr/bin/python3.6 /opt/mozdef/envs/python && \
  source /opt/mozdef/envs/python/bin/activate && \
  pip install --requirement /opt/mozdef/envs/mozdef/requirements.txt && \
  cd /opt/mozdef/envs/mozdef/mozdef_util && \
  pip install --editable . && \
  mkdir /opt/mozdef/envs/mozdef/data


WORKDIR /opt/mozdef/envs/mozdef

VOLUME /opt/mozdef/envs/mozdef/data

# Automatically source into python virtual environment
ENV PATH=/opt/mozdef/envs/python/bin:$PATH

USER root
