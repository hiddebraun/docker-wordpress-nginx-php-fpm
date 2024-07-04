FROM php:8.1-fpm-alpine

RUN apk update && apk add --update \
    icu-dev \
    oniguruma-dev \
    linux-headers \
    pcre-dev \
    libxml2-dev \
    libzip-dev zip \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    ${PHPIZE_DEPS}

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN docker-php-ext-configure intl && docker-php-ext-install intl
RUN docker-php-ext-install mbstring && docker-php-ext-configure zip
RUN docker-php-ext-install soap && docker-php-ext-enable soap
RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd && docker-php-ext-enable gd
RUN docker-php-ext-install pdo mysqli pdo_mysql

RUN pecl install xdebug-3.3.2
