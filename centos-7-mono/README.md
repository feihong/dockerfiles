# CentOS 7 for F#

This helps you compile mono to deploy on WebFaction.

## Prerequisites

    wget http://download.mono-project.com/sources/mono/mono-5.10.1.47.tar.bz2
    tar jxf mono-5.10.1.47.tar.bz2

Source: https://gist.github.com/andreazevedo/9479518

## Build

    docker build -t centos-7-mono .

## Run

    docker run -it --mount type=bind,source=$PWD,target=/src centos-7-mono

## Compile Mono

Once inside the container, run:

    cd /src/mono-5.10.1.47
    ./configure
    make && make install

Compilation will take a pretty good amount of time.

Source: http://www.mono-project.com/docs/compiling-mono/linux/

## Run program inside CentOS container

    docker run -it -p 8001:8001 \
      --mount type=bind,source=$HOME/work/fsharp-quickstart,target=/src \
      centos-7-mono \
      mono server.exe
