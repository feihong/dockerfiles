FROM centos:7

WORKDIR /src

ENV LANG "en_US.UTF-8"
ENV ELIXIR_VERSION 1.6.4

RUN yum -y update \
    && yum install -y epel-release \
    && yum install -y wget gcc gcc-c++ glibc-devel make ncurses-devel openssl-devel autoconf java-1.8.0-openjdk-devel git \
    && wget http://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm \
    && rpm -Uvh erlang-solutions-1.0-1.noarch.rpm \
    && yum install -y erlang \
    && wget https://github.com/elixir-lang/elixir/archive/v$ELIXIR_VERSION.tar.gz \
    && tar xvfz v$ELIXIR_VERSION.tar.gz -C /opt \
    && cd /opt/elixir-$ELIXIR_VERSION \
    && make clean test \
    && ln -s /opt/elixir-$ELIXIR_VERSION/bin/iex /usr/bin/iex \
    && ln -s /opt/elixir-$ELIXIR_VERSION/bin/mix /usr/bin/mix \
    && ln -s /opt/elixir-$ELIXIR_VERSION/bin/elixir /usr/bin/elixir \
    && ln -s /opt/elixir-$ELIXIR_VERSION/bin/elixirc /usr/bin/elixirc

CMD ["/bin/bash"]
