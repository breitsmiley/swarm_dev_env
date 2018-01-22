FROM php:7.2.1-fpm-alpine3.7


COPY /docker/c-bc-php/php.ini /usr/local/etc/php/php.ini
COPY /docker/c-bc-php/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Use multi-stage builds https://docs.docker.com/engine/userguide/eng-image/multistage-build/
# TODO контролировать конечную версию alpine $ cat /etc/alpine-release  
COPY --from=composer:1.6.2 /usr/bin/composer /usr/bin/composer

# Installing
# GIT
# Xdebug - https://github.com/xdebug/xdebug (deppends on g++ make autoconf)
RUN apk update \
    && apk add  --no-cache git
RUN apk add --no-cache --virtual build-dependencies icu-dev \
    g++ make autoconf \
    && git clone https://github.com/xdebug/xdebug.git /tmp/xdebug \
    && cd /tmp/xdebug \
    && sh ./rebuild.sh \
    && apk del build-dependencies \
    && rm -rf /tmp/*

WORKDIR /usr/src/bc

# делаем сборку
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN composer global require "hirak/prestissimo:^0.3" --prefer-dist --no-progress --no-suggest --classmap-authoritative

COPY /apps/book-collector/composer.* ./
RUN composer install --prefer-dist --no-dev --no-autoloader --no-scripts --no-progress --no-suggest \
	&& composer clear-cache

COPY /apps/book-collector ./

# todo решить вопрос с правами
# RUN mkdir -p var/cache var/logs var/sessions \
# 	&& composer dump-autoload --classmap-authoritative --no-dev \
# 	&& chown -R www-data var