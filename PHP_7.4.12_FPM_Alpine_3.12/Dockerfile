FROM php:7.4.12-fpm-alpine3.12
LABEL maintainer="Gilson Gabriel <gilson@codemastersolucoes.com>"

RUN apk add --no-cache shadow nano git unzip supervisor composer libxml2-dev libxslt-dev oniguruma-dev libzip-dev icu-dev \
    unixodbc-dev autoconf make build-base \
    && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
    && docker-php-ext-install intl bcmath json pdo pdo_mysql xml xmlrpc xsl mbstring zip pcntl redis mysqli \
    && rm -rf /var/www/html \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apk/*

RUN curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.2-1_amd64.apk

RUN apk add --allow-untrusted msodbcsql17_17.5.2.2-1_amd64.apk

RUN pecl install sqlsrv pdo_sqlsrv xdebug-2.9.6 \
    && docker-php-ext-enable \
    sqlsrv pdo_sqlsrv xsl zip xdebug intl bcmath json pdo pdo_mysql xml xmlrpc mbstring pcntl redis mysqli

RUN rm -rf msodbcsql17_17.5.2.2-1_amd64.apk

ENV DV v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DV/dockerize-linux-amd64-$DV.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DV.tar.gz \
    && rm dockerize-linux-amd64-$DV.tar.gz

RUN composer global require spatie/phpunit-watcher

RUN apk del --purge libxml2-dev oniguruma-dev unixodbc-dev autoconf make build-base

COPY ./supervisord.conf /etc/
COPY ./docker-php-entrypoint /usr/local/bin/
COPY ./docker-php-entrypoint /usr/local/bin/entrypoint
RUN chmod +x /usr/local/bin/docker-php-entrypoint
RUN chmod +x /usr/local/bin/entrypoint

EXPOSE 9000
EXPOSE 9001
