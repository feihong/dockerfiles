FROM centos:7

RUN rpm --import "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" \
  && curl https://download.mono-project.com/repo/centos7-stable.repo | tee /etc/yum.repos.d/mono-centos7-stable.repo \
  && yum -y update \
  && yum install -y mono-devel gcc gcc-c++ autoconf libtool automake cmake make gettext which

WORKDIR /src

CMD ["/bin/bash"]
