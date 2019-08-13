FROM leroymerlinbr/php:7.3-fpm-nginx

USER root

RUN docker-php-ext-enable xdebug

COPY custom.ini /usr/local/etc/php/conf.d/

USER www-data:www-data
