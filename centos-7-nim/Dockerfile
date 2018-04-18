FROM centos:7

RUN yum install -y gcc git \
    && curl https://nim-lang.org/download/nim-0.18.0.tar.xz -o nim.tar.xz \
    && tar xvf nim.tar.xz \
    && cd nim-0.18.0 \
    && sh build.sh \
    && bin/nim c koch \
    && ./koch tools \
    && ln -s /nim-0.18.0/bin/nim /usr/bin/nim \
    && ln -s /nim-0.18.0/bin/nimble /usr/bin/nimble

WORKDIR /src

CMD ["/bin/bash"]
