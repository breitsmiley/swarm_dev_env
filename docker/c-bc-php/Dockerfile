
FROM php:7.2.1-fpm-alpine3.7

# Use multi-stage builds https://docs.docker.com/engine/userguide/eng-image/multistage-build/
# TODO контролировать конечную версию alpine $ cat /etc/alpine-release 
COPY --from=composer:1.6.2 /usr/bin/composer /usr/bin/composer

# RUN mkdir -p /usr/src/bc
COPY . /usr/src/bc
WORKDIR /usr/src/bc
# CMD [ "php", "./your-script.php" ]


# # auxiliary env
# #---------------------------
# ENV COMPOSER_VERSION=1.5.5 
# #---------------------------

# # Custom php.ini
# COPY /docker/book-collector-php/php.ini /usr/local/etc/php/


# # COPY /apps/book-collector/web /srv/blog/public

# # Changing Apache's DocumentRoot
# #----------------------------------------------------
# # RUN mkdir -p /var/www/book-collector/public
# ENV APACHE_DOCUMENT_ROOT /var/www/book-collector/public

# RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
# RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
# #----------------------------------------------------


# # Install Composer
# #----------------------------------------------------
# ENV PATH="/composer/vendor/bin:$PATH" \
#     COMPOSER_ALLOW_SUPERUSER=1 \
#     COMPOSER_VENDOR_DIR=/var/www/vendor \
#     COMPOSER_HOME=/composer
# RUN curl -s -f -L -o /tmp/installer.php https://raw.githubusercontent.com/composer/getcomposer.org/da290238de6d63faace0343efbdd5aa9354332c5/web/installer \
#  && php -r " \
#     \$signature = '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410'; \
#     \$hash = hash('SHA384', file_get_contents('/tmp/installer.php')); \
#     if (!hash_equals(\$signature, \$hash)) { \
#         unlink('/tmp/installer.php'); \
#         echo 'Integrity check failed, installer is either corrupt or worse.' . PHP_EOL; \
#         exit(1); \
#     }" \
#  && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} \
#  && rm /tmp/installer.php \
#  && composer --ansi --version --no-interaction
#  #----------------------------------------------------

# # # Copy project files
# # COPY /apps/book-collector /var/www/book-collector

# # WORKDIR /srv/api
# #  # install composer dependencies
# # WORKDIR /var/www/book-collector
# # COPY ./composer.json ./composer.lock ./
# # ENV COMPOSER_VENDOR_DIR=/var/www/vendor
# # # RUN composer config github-oauth.github.com YOUROAUTHKEYHERE
# # RUN composer install --no-scripts --no-autoloader --ansi --no-interaction

# WORKDIR /var/www/book-collector
# # Copy project files
# COPY . .
# # Install Composer dependencies
# COPY composer.json composer.lock ./
# RUN composer install --prefer-dist --no-dev --no-autoloader --no-scripts --no-progress --no-suggest \
# 	&& composer clear-cache