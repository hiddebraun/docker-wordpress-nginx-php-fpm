FROM php:7.4-fpm

RUN pecl install xdebug-3.1.5
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
