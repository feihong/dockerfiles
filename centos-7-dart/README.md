# CentOS 7 with Dart installed

This is for compiling the Dart standalone executable to run on WebFaction.

Source: [Building Dart on CentOS, Red Hat, Fedora and Amazon Linux AMI](https://github.com/dart-lang/sdk/wiki/Building-Dart-on-CentOS,-Red-Hat,-Fedora-and-Amazon-Linux-AMI)

## Download source

    cd ~/src
    git clone https://chromium.googlesource.com/chromium/tools/depot_tools

Note: Don't clone the dart-lang/sdk repo. Running the `fetch` command inside the container will fetch all the files you need.

## Build

    docker build -t centos-7-dart .

## Run

    docker run -it --mount type=bind,source=$HOME/src,target=/src centos-7-dart

## Compile standalone executable

Once inside the container, run:

    export PATH=$PATH:/src/depot_tools
    mkdir dart-sdk
    cd dart-sdk
    fetch dart
    cd sdk
    git checkout 2.0.0-dev.49.0
    tools/build.py --mode=release --arch=x64 runtime

The fetch step actually takes a really long time because it will download something like 10 GB (!). It may actually error out (for me, it was unable to install some fuchsia thing). Regardless, proceed with the build step.

The tag you checkout should match what you get when you run `dart --version` on your host machine. If the version doesn't match, you will not be able to run snapshots built by other versions of Dart. However, you will still be able to execute source files.

The build will generally take less than an hour. Once the build has completed, the standalone executable can be found at `out/ReleaseX64/dart`.
