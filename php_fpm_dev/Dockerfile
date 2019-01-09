FROM php:7.1-fpm-alpine

RUN apk add --no-cache --virtual .build-deps \
        g++ \
        make \
        autoconf \
    && apk add --no-cache \
        libpng-dev \
        imap-dev \
        nginx \
        nano \
        zip \
        unzip \
        supervisor \
        git \
        nodejs \
        nodejs-npm \
        python \
    && curl -fsSL 'http://apache.cp.if.ua/zookeeper/stable/zookeeper-3.4.12.tar.gz' -o zookeeper.tar.gz \
        && mkdir -p /tmp/zookeeper \
        && tar -xf zookeeper.tar.gz -C /tmp/zookeeper --strip-components=1 \
        && rm zookeeper.tar.gz \
        && (\
          cd /tmp/zookeeper/src/c \
          &&  ./configure \
          &&  make install \
        ) \
        && pecl install zookeeper \
        && rm -r /tmp/zookeeper \
    &&  docker-php-ext-install \
        pdo_mysql \
        gd \
        zip \
        imap \
    && docker-php-ext-enable \
        zookeeper \
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && apk del .build-deps
