FROM php:7.4.4-fpm-alpine3.11
MAINTAINER "Gilson Gabriel <gilson@codemastersolucoes.com>"

RUN apk add --no-cache libzip-dev libxml2-dev libxslt-dev oniguruma-dev nano git unzip supervisor composer \
    && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
    && docker-php-ext-install bcmath json pdo pdo_mysql xml xmlrpc xsl mbstring zip pcntl redis \
    && rm -rf /var/www/html \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apk/*

ENV DV v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DV/dockerize-linux-amd64-$DV.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DV.tar.gz \
    && rm dockerize-linux-amd64-$DV.tar.gz

COPY ./supervisord.conf /etc/
COPY ./docker-php-entrypoint /usr/local/bin/
COPY ./docker-php-entrypoint /usr/local/bin/entrypoint
RUN chmod +x /usr/local/bin/docker-php-entrypoint
RUN chmod +x /usr/local/bin/entrypoint

WORKDIR /app

EXPOSE 9000
EXPOSE 9001