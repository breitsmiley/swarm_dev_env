
FROM php:7.2.1-fpm-alpine3.7

# Use multi-stage builds https://docs.docker.com/engine/userguide/eng-image/multistage-build/
# TODO контролировать конечную версию alpine $ cat /etc/alpine-release  
COPY --from=composer:1.6.2 /usr/bin/composer /usr/bin/composer

# RUN mkdir -p /usr/src/bc

RUN apk add --no-cache --virtual .persistent-deps \
		git 
		# icu-libs \
		# libpq \
		# zlib


WORKDIR /usr/src/bc

# Prevent the reinstallation of vendors at every changes in the source code
ENV COMPOSER_ALLOW_SUPERUSER 1
COPY /apps/book-collector/composer.* ./
RUN composer install --prefer-dist --no-dev --no-autoloader --no-scripts --no-progress --no-suggest \
	&& composer clear-cache

COPY . ./

# RUN mkdir -p var/cache var/logs var/sessions \
# 	&& composer dump-autoload --classmap-authoritative --no-dev \
# 	&& chown -R www-data var