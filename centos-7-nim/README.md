# CentOS 7 with nim installed

This is useful for compiling a binary to deploy on WebFaction.

## Build

    docker build -t centos-7-nim .
    
## Run

    docker run -it --mount type=bind,source=$HOME/work/nim-quickstart,target=/src centos-7-nim
