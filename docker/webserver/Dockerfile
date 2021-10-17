FROM php:8.0.2-apache

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y \
        libzip-dev \
        zip \
        libxml2-dev  \
        openssl  \
        libssl-dev  \
        libcurl4-openssl-dev \
  && docker-php-ext-install zip

RUN apt-get autoremove -y && apt-get autoclean

RUN pecl install mongodb
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
RUN echo "extension=mongodb.so" > /usr/local/etc/php/php.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

