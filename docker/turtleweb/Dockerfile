FROM nginx:1.15.2

RUN apt-get update \
  && apt-get install -y git \
  && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/turtlecoin/turtle-pool \
  && mv turtle-pool/website/* /usr/share/nginx/html

ADD config.js /usr/share/nginx/html

EXPOSE 80
EXPOSE 443