FROM ubuntu:xenial

MAINTAINER Jozhe <jozhe@energo.cn>

RUN apt-get update \
     && apt-get install -y wget \
     && rm -rf /var/lib/apt/lists/* 

WORKDIR "/opt"
ARG BINARY="geth-linux-amd64-1.8.8-2688dab4.tar.gz"
RUN wget "https://gethstore.blob.core.windows.net/builds/$BINARY"
RUN tar -xzvf $BINARY --strip 1
RUN rm $BINARY

ADD ./genesis.json ./genesis.json
RUN ./geth init genesis.json

ARG password
ARG privatekey
RUN echo $password > ~/.password
RUN echo $privatekey > ~/.privatekey
RUN ./geth account import --password ~/.password  ~/.privatekey

ENV address=""
ENV bootnodeId=""
ENV bootnodeIp=""
CMD exec ./geth --syncmode 'full' --port 30313 --rpc --rpcaddr '0.0.0.0' --rpcport 8503 --rpcapi 'personal,db,eth,net,web3,txpool,miner' --bootnodes "enode://$bootnodeId@$bootnodeIp:30311" --networkid="1005" --gasprice '1' -unlock $address --password ~/.password --mine

EXPOSE 8503
EXPOSE 30313
