# CentOS 7 with Dart installed

This is for compiling the Dart standalone executable to run on WebFaction.

Source: [Building Dart on CentOS, Red Hat, Fedora and Amazon Linux AMI](https://github.com/dart-lang/sdk/wiki/Building-Dart-on-CentOS,-Red-Hat,-Fedora-and-Amazon-Linux-AMI)

## Download source

    cd ~/src
    git clone https://chromium.googlesource.com/chromium/tools/depot_tools
    git clone https://github.com/dart-lang/sdk dart-sdk

## Build

    docker build -t centos-7-dart .

## Run

    docker run -it --mount type=bind,source=$HOME/src,target=/src centos-7-dart

## Compile release build

Once inside the container, run:

    export PATH=$PATH:/src/depot_tools
    mkdir dart-sdk
    cd dart-sdk
    fetch dart
    tools/build.py --mode=release --arch=x64 runtime

The fetch step actually takes a really long time.

The standalone executable should be at `out/ReleaseX64/dart`.
