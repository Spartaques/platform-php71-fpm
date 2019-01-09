FROM php:7.1-fpm-alpine

RUN apk add --no-cache --virtual .build-deps \
        g++ \
        make \
        autoconf \
    && apk add --no-cache \
        nginx \
        nano \
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
        opcache \
        pdo_mysql \
    && docker-php-ext-enable \
        zookeeper \
        opcache \
        pdo_mysql \
    && apk del .build-deps


  RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
