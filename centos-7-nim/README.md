# CentOS 7 with Nim installed

This is useful for compiling a binary to deploy on WebFaction.

## Build

    docker build -t centos-7-nim .

## Run

    docker run -it --mount type=bind,source=$HOME/work/nim-quickstart,target=/src centos-7-nim

## Compile release build

    docker run -it \
      --mount type=bind,source=$HOME/work/nim-quickstart,target=/src \
      centos-7-nim \
      nim c -d:release server.nim

## Run program inside CentOS container

    docker run -it -p 8001:8001 \
      --mount type=bind,source=$HOME/work/nim-quickstart,target=/src \
      centos-7-nim \
      ./server
