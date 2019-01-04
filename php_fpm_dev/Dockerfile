FROM php:7.1-fpm-alpine

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        libpng-dev \
        libmcrypt-dev \
        libtool \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
    && apk add --no-cache \
        curl \
        git \
        imagemagick \
        libmcrypt \
        mysql-client \
        postgresql-libs \
        libintl \
        icu \
        icu-dev \
        autoconf \
    && pecl install imagick \
    && docker-php-ext-install \
        curl \
        iconv \
        mbstring \
        mcrypt \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pcntl \
        tokenizer \
        xml \
        zip \
        intl \
        gd

RUN docker-php-ext-enable imagick \
    && apk add imap-dev \
    && docker-php-ext-install imap \
    && docker-php-ext-enable imap \
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && apk del -f .build-deps

RUN apk update \
    && apk add --no-cache \
        nginx \
        nano \
        curl \
        supervisor \
        git \
        zip \
        unzip \
        openssl-dev \
        g++ \
        make \
        nodejs \
        nodejs-npm \
        python

RUN wget http://apache.cp.if.ua/zookeeper/stable/zookeeper-3.4.12.tar.gz \
    && tar --extract --gzip --file zookeeper-3.4.12.tar.gz \
    && cd zookeeper-3.4.12/src/c \
    && ./configure \
    && make install \
    && pecl install zookeeper \
    && rm -rf zookeeper-3.4.12.tar.gz zookeeper-3.4.12 \
    && docker-php-ext-enable zookeeper

RUN apk del && rm -f /var/cache/apk/*
