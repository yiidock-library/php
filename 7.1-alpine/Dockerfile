FROM php:7.1-alpine

MAINTAINER Alexey Samoylov <alexey.samoylov@gmail.com>

# add run deps
RUN apk add --no-cache --virtual .rundeps \
icu-libs \
freetype \
libjpeg-turbo \
libpng \
libmcrypt \
libxml2 \
zlib \
libpq \
sqlite-libs \
openssl \
ca-certificates \
&& update-ca-certificates    

# add build deps that will be removed
RUN apk add --no-cache --virtual .builddeps \
$PHPIZE_DEPS \
icu-dev \
libjpeg-turbo-dev \
libpng-dev \
freetype-dev \
zlib-dev \
libmcrypt-dev \
libxml2-dev \
sqlite-dev \
postgresql-dev \
#
# add php extensions
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ \
&& docker-php-ext-install \
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
json \
#
# cleanup to keep the images size small
&& apk del --no-cache .builddeps

ADD yii.ini $PHP_INI_DIR/conf.d/

# Install composer
COPY install-composer.sh /
RUN sh /install-composer.sh && rm /install-composer.sh
