FROM php:8.1-fpm-alpine3.15

RUN apk add --update \
        shadow\
        autoconf \
        zlib-dev \
        icu-dev \
        build-base \
        libzip-dev \
    && docker-php-ext-install opcache \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install intl \
    && rm -rf /tmp/* /var/cache/apk/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
    && mkdir /usr/local/opt

###
### Configure
###
RUN set -ex \
	&& test ! -d /var/lib/php/sessions && mkdir -p /var/lib/php/sessions \
	&& chown www-data:www-data /var/lib/php/sessions

###
### Optimize symfony performance: https://symfony.com/doc/4.1/performance.html
###
COPY opcache.ini /usr/local/etc/php/conf.d
COPY realpath_cache.ini /usr/local/etc/php/conf.d

ARG UID
ARG GID
RUN usermod -u "$UID" www-data \
    && groupmod -g "$GID" www-data \
    && usermod -m -d /home/www-data www-data
