FROM centos:7

RUN yum -y update \
    && yum install -y gcc gcc-c++ autoconf libtool automake cmake gettext which

WORKDIR /src

CMD ["/bin/bash"]
