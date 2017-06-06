FROM php:5-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev g++ libicu-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install intl \
    && apt-get purge --auto-remove -y g++
