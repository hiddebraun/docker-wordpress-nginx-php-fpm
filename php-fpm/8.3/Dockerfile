FROM php:8.3-fpm-alpine

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
    imagemagick-dev \
    ${PHPIZE_DEPS}

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN docker-php-ext-configure intl && docker-php-ext-install intl
RUN docker-php-ext-install mbstring && docker-php-ext-enable mbstring
RUN docker-php-ext-install zip && docker-php-ext-enable zip
RUN docker-php-ext-install soap && docker-php-ext-enable soap
RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd && docker-php-ext-enable gd
RUN docker-php-ext-install pdo mysqli pdo_mysql
RUN docker-php-ext-install exif && docker-php-ext-enable exif

# Imagick PHP 8.3 exception: https://orkhan.dev/2024/02/07/using-imagick-with-php-83-on-docker/
RUN apk add git --update --no-cache && \
    git clone https://github.com/Imagick/imagick.git --depth 1 /tmp/imagick && \
    cd /tmp/imagick && \
    git fetch origin master && \
    git switch master && \
    cd /tmp/imagick && \
    phpize && \
    ./configure && \
    make && \
    make install && \
    apk del git && \
    docker-php-ext-enable imagick

RUN pecl install xdebug-3.3.2
