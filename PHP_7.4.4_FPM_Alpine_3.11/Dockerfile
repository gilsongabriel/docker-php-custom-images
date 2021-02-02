FROM php:7.4.4-fpm-alpine3.11
LABEL maintainer="Gilson Gabriel <gilson@codemastersolucoes.com>"

RUN apk add --no-cache shadow libzip-dev libxml2-dev libxslt-dev oniguruma-dev nano git unzip supervisor composer icu-dev \
    && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
    && docker-php-ext-install bcmath json pdo pdo_mysql xml xmlrpc xsl mbstring zip pcntl redis intl \
    && rm -rf /var/www/html \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apk/*

ENV DV v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DV/dockerize-linux-amd64-$DV.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DV.tar.gz \
    && rm dockerize-linux-amd64-$DV.tar.gz

RUN docker-php-ext-enable intl

RUN apk del --purge libxml2-dev oniguruma-dev

RUN wget https://github.com/deluan/zsh-in-docker/releases/download/v1.1.1/zsh-in-docker.sh

RUN chmod +x zsh-in-docker.sh

RUN ./zsh-in-docker.sh \
    -t https://github.com/denysdovhan/spaceship-prompt \
    -a 'SPACESHIP_PROMPT_ADD_NEWLINE="false"' \
    -a 'SPACESHIP_PROMPT_SEPARATE_LINE="false"' \
    -p git \
    -p https://github.com/zsh-users/zsh-autosuggestions \
    -p https://github.com/zsh-users/zsh-completions \
    -p https://github.com/zsh-users/zsh-history-substring-search \
    -p https://github.com/zsh-users/zsh-syntax-highlighting \
    -p 'history-substring-search' \
    -a 'bindkey "\$terminfo[kcuu1]" history-substring-search-up' \
    -a 'bindkey "\$terminfo[kcud1]" history-substring-search-down'

# COPY ./zshrc ~/.zshrc

RUN apk add --no-cache zsh-vcs

COPY ./supervisord.conf /etc/
COPY ./docker-php-entrypoint /usr/local/bin/
COPY ./docker-php-entrypoint /usr/local/bin/entrypoint
RUN chmod +x /usr/local/bin/docker-php-entrypoint
RUN chmod +x /usr/local/bin/entrypoint

EXPOSE 9000
EXPOSE 9001
