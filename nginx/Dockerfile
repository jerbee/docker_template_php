FROM debian:jessie

RUN truncate -s 0 /etc/apt/sources.list
RUN echo "deb http://mirrors.digitalocean.com/debian/ jessie main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.digitalocean.com/debian/ jessie-updates main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.digitalocean.com/debian/ jessie-backports main" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    nginx

ADD nginx.conf /etc/nginx/

ADD default /etc/nginx/sites-available/

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
