FROM ubuntu:xenial

MAINTAINER Jozhe <jozhe@energo.cn>

RUN apt-get update \
     && apt-get install -y wget \
     && rm -rf /var/lib/apt/lists/* 

WORKDIR "/opt"
ARG BINARY="geth-alltools-linux-amd64-1.8.8-2688dab4.tar.gz"
RUN wget "https://gethstore.blob.core.windows.net/builds/$BINARY"
RUN tar -xzvf $BINARY --strip 1
RUN rm $BINARY

ENV nodekeyhex=""
CMD exec ./bootnode -nodekeyhex $nodekeyhex -verbosity 4 -addr :30311

EXPOSE 30311/udp
