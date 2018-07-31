FROM debian:9 as builder

#VOLUME ["/var/lib/turtlecoind", "/home/turtlecoin","/var/log/turtlecoind"]
#ARG TURTLECOIN_VERSION=v0.2.2

# install build dependencies
# checkout the latest tag
# build and install
RUN apt-get update && \
    apt-get install -y \
      build-essential \
      gdb \
      libreadline-dev \
      python-dev \
      gcc \
      g++\
      git \
      cmake \
      libboost-all-dev \
      librocksdb-dev && \
    git clone -b master https://github.com/turtlecoin/turtlecoin /opt/turtlecoin && \
    cd /opt/turtlecoin && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make

FROM debian:9

# TurtleCoind now needs libreadline 
RUN apt-get update && \
    apt-get install -y \
      libreadline-dev \
     && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/local/bin && mkdir -p /tmp/checkpoints 

WORKDIR /usr/local/bin
COPY --from=builder /opt/turtlecoin/build/src/TurtleCoind .
COPY --from=builder /opt/turtlecoin/build/src/service .
COPY --from=builder /opt/turtlecoin/build/src/zedwallet .
COPY --from=builder /opt/turtlecoin/build/src/miner .
RUN mkdir -p /var/lib/turtlecoind
WORKDIR /var/lib/turtlecoind
ADD https://github.com/turtlecoin/checkpoints/raw/master/checkpoints.csv /tmp/checkpoints/
ENTRYPOINT ["/usr/local/bin/TurtleCoind"]
CMD ["--no-console","--data-dir","/var/lib/turtlecoind","--rpc-bind-ip","0.0.0.0","--rpc-bind-port","11898","--p2p-bind-port","11897","--enable-cors=*","--enable_blockexplorer","--load-checkpoints","/tmp/checkpoints/checkpoints.csv"]