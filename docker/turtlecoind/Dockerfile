FROM ubuntu:xenial

RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*

ENV TURTLE_VERSION=0.6.3 

WORKDIR /home/turtlecoin

RUN curl -OL https://github.com/turtlecoin/turtlecoin/releases/download/v${TURTLE_VERSION}/turtlecoin-v${TURTLE_VERSION}-linux.tar.gz && \
    tar -xvzf turtlecoin-v${TURTLE_VERSION}-linux.tar.gz &&\
    mv turtlecoin-v${TURTLE_VERSION}/* . &&\
    rm -rf turtlecoin-v${TURTLE_VERSION} &&\
    curl -OL https://github.com/turtlecoin/checkpoints/raw/master/checkpoints.csv

ENTRYPOINT ["./TurtleCoind"]
CMD ["--no-console","--data-dir","/var/lib/turtlecoind","--rpc-bind-ip","0.0.0.0","--rpc-bind-port","11898","--p2p-bind-port","11897","--enable-cors=*","--enable_blockexplorer","--load-checkpoints","checkpoints.csv"]