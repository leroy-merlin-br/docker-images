FROM php:7.4-fpm-buster
LABEL maintainer="boitata@leroymerlin.com.br"

# libssl-dev: required by mongodb
# libzip-dev: required by zip
# zlib1g-dev: required by zip
RUN apt-get update -qq \
  && apt-get install -qq --no-install-recommends \
    git \
    zip \
    unzip \
    libzip-dev \
    libssl-dev \
    zlib1g-dev \
 && apt-get clean

RUN pecl install mongodb \
  && pecl install xdebug \
  && docker-php-ext-enable \
    mongodb \
  && docker-php-ext-install \
    pcntl \
    zip \
  && rm -rf /tmp/*

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN sed -ri -e 's!user = www-data!; user = www-data!g' /usr/local/etc/php-fpm.d/www.conf \
  && sed -ri -e 's!group = www-data!; group = www-data!g' /usr/local/etc/php-fpm.d/www.conf

ARG UID=1000
ARG GID=1000

RUN groupmod -g ${GID} www-data \
  && usermod -u ${UID} -g www-data www-data \
  && mkdir -p /var/www/html \
  && chown -hR www-data:www-data \
    /var/www \
    /usr/local/

USER www-data:www-data
WORKDIR /var/www/html
ENV PATH=$PATH:/var/www/.composer/vendor/bin
