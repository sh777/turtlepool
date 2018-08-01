FROM nginx:1.15.2

RUN apt-get update \
  && apt-get install -y git \
  && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/turtlecoin/turtle-pool \
  && mv website/* /usr/share/nginx/html

ADD config/config.js /usr/share/nginx/html

EXPOSE 80
EXPOSE 443