# CentOS 7 for F#

This helps you compile mono to deploy on WebFaction.

## Prerequisites

    export MONO_VERSION=5.10.1.47
    git clone https://github.com/mono/mono mono-src
    git checkout mono-$MONO_VERSION

## Build the container

    docker build -t centos-7-mono .

## Start the container

    export SERVER_PREFIX=/home/fhsu/mono
    docker run -it \
      -e "SERVER_PREFIX=$SERVER_PREFIX"
      --mount type=bind,source=`pwd`,target=/src \
      --mount type=bind,source=`pwd`/output,target=$SERVER_PREFIX  \
      centos-7-mono

## Compile Mono

Once inside the container, run:

    cd /src/mono-src
    ./autogen.sh --prefix=$SERVER_PREFIX
    make
    make install

Note that both `make` and `make install` commands take a really long time.

Source: http://www.mono-project.com/docs/compiling-mono/linux/#building-mono-from-a-git-source-code-checkout

## Run program inside CentOS container

    export SERVER_PREFIX=/home/fhsu
    docker run -it -p 8001:8001 \
      -e "SERVER_PREFIX=$SERVER_PREFIX" \
      --mount type=bind,source=`pwd`/output,target=$SERVER_PREFIX \
      --mount type=bind,source=$HOME/work/fsharp-quickstart,target=/src \
      centos-7-mono \
      $SERVER_PREFIX/bin/mono server.exe
