FROM centos:7

WORKDIR /src

RUN yum -y update \
    && yum install -y epel-release \
    && yum install -y wget gcc gcc-c++ glibc-devel make ncurses-devel openssl-devel autoconf java-1.8.0-openjdk-devel \
    && wget http://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm \
    && rpm -Uvh erlang-solutions-1.0-1.noarch.rpm
    && yum install -y erlang \
    && wget https://github.com/elixir-lang/elixir/archive/v1.6.4.tar.gz \
    && tar xvfz v1.6.4.tar.gz -C /opt
    && cd /opt/elixir-1.6.4 \
    && make clean test \
    && ln -s /opt/elixir-1.6.4/bin/iex /usr/bin/iex \
    && ln -s /opt/elixir-1.6.4/bin/mix /usr/bin/mix \
    && ln -s /opt/elixir-1.6.4/bin/elixir /usr/bin/elixir \
    && ln -s /opt/elixir-1.6.4/bin/elixirc /usr/bin/elixirc

CMD ["/bin/bash"]
