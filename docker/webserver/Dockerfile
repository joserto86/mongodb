FROM php:8.0.2-apache

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y libxml2-dev openssl libssl-dev libcurl4-openssl-dev
RUN apt-get autoremove -y && apt-get autoclean

RUN pecl install mongodb
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
RUN echo "extension=mongodb.so" > /usr/local/etc/php/php.ini

COPY --from=composer /usr/bin/composer /usr/bin/composer

