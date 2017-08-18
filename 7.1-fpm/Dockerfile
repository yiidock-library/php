FROM php:7.1-fpm

MAINTAINER Alexey Samoylov <alexey.samoylov@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y \
&& apt-get install -y \
libxml2-dev \
libfreetype6-dev \
libjpeg62-turbo-dev \
libpng12-dev \
libicu-dev \
libmcrypt-dev \
libpq-dev \
libsqlite3-dev

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) \
gd \
intl \
mcrypt \
pdo \
pdo_mysql \
pdo_pgsql \
pdo_sqlite \
fileinfo \
mbstring \
dom \
opcache \
zip \
json 

RUN apt-get purge -y \
libxml2-dev \
libfreetype6-dev \
libjpeg62-turbo-dev \
libpng12-dev \
libicu-dev \
libmcrypt-dev \
libpq-dev \
libsqlite3-dev \
comerr-dev \
icu-devtools \
libssl-dev \
libssl-doc \
zlib1g-dev \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
