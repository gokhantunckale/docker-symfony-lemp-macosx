FROM ubuntu:16.04

MAINTAINER mhtkpt@gmail.com

ARG DEBIAN_FRONTEND=noninteractive
ARG TIMEZONE=Europe/Istanbul

RUN apt-get update \
    \
    &&  apt-get install -y \
    \
    software-properties-common \
    python-software-properties \
    curl \
    vim \
    wget \
    unzip \
    net-tools

RUN LC_ALL=C.UTF-8 add-apt-repository -y -u ppa:ondrej/php \
    \
    && apt-get update \
    \
    && apt-get -y install --quiet \
    \
    imagemagick \
    graphicsmagick \
    \
    nginx \
    \
    php7.2-bcmath \
    php7.2-bz2 \
    php7.2-cli \
    php7.2-common \
    php7.2-curl \
    php7.2-dba \
    php7.2-fpm \
    php7.2-gd \
    php7.2-gmp \
    php7.2-imap \
    php7.2-intl \
    php7.2-ldap \
    php7.2-mbstring \
    php7.2-mysql \
    php7.2-odbc \
    php7.2-pgsql \
    php7.2-recode \
    php7.2-snmp \
    php7.2-soap \
    php7.2-sqlite \
    php7.2-tidy \
    php7.2-xml \
    php7.2-xmlrpc \
    php7.2-xsl \
    php7.2-zip \
    php-gnupg \
    php-imagick \
    php-streams \
    php-fxsl \
    \
    && apt-get -y autoremove \
    \
    && apt-get -y autoclean \
    \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | /usr/bin/php -- --install-dir=/usr/local/bin --filename=composer creates=/usr/local/bin/composer

ADD conf/nginx.conf /etc/nginx/
ADD conf/phpmyadmin.conf /etc/nginx/
ADD conf/symfony.conf /etc/nginx/conf.d/
ADD conf/symfony_dev.conf /etc/nginx/conf.d/

RUN rm -rf /etc/nginx/sites-available
RUN rm -rf /etc/nginx/sites-enabled

RUN \
    sed -i -e 's/max_execution_time = 30/max_execution_time = 300/g' /etc/php/7.2/fpm/php.ini && \
    sed -i -e 's/upload_max_filesize = 2M/upload_max_filesize = 256M/g' /etc/php/7.2/fpm/php.ini && \
    sed -i -e 's/post_max_size = 8M/post_max_size = 512M/g' /etc/php/7.2/fpm/php.ini && \
    sed -i -e 's/memory_limit = 128M/memory_limit = 8G/g' /etc/php/7.2/fpm/php.ini

WORKDIR /var/www
