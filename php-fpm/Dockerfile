FROM php:8.1.19-fpm

RUN pecl install xdebug-3.2.1 && docker-php-ext-enable xdebug
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
