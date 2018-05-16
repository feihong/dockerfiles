# CentOS 7 for Mono

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
      -e "SERVER_PREFIX=$SERVER_PREFIX" \
      --mount type=bind,source=`pwd`,target=/src \
      --mount type=bind,source=`pwd`/output,target=$SERVER_PREFIX  \
      centos-7-mono

## Compile Mono

Once inside the container, run:

    cd /src/mono-src
    ./autogen.sh --prefix=$SERVER_PREFIX
    make clean
    make
    make install

Note that `autogen.sh` finishes pretty quickly, but both `make` and `make install` take a really long time. You only need to run `make clean` if you get errors like  `ln: failed to create symbolic link '/src/mono-src/mcs/class/lib/build': File exists`.

Install mono to server:

    tar cvfz mono.tar.gz output
    scp mono.tar.gz user.webfactional.com/~
    ssh user.webfactional.com
    tar xvfz mono.tar.gz
    mv output mono
    ln -s $HOME/mono/bin/mono $HOME/bin/mono

Source: http://www.mono-project.com/docs/compiling-mono/linux/#building-mono-from-a-git-source-code-checkout

## Run program inside CentOS container

    export SERVER_PREFIX=/home/fhsu/mono
    docker run -it -p 8001:8001 \
      -e "SERVER_PREFIX=$SERVER_PREFIX" \
      --mount type=bind,source=`pwd`/output,target=$SERVER_PREFIX \
      --mount type=bind,source=$HOME/work/fsharp-quickstart,target=/src \
      centos-7-mono \
      $SERVER_PREFIX/bin/mono server.exe
