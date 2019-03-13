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

RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
    \
    && apt-get update \
    \
    && apt-get -y install --quiet \
    nginx \
    php7.3 \
    php7.3-bcmath \
    php7.3-bz2 \
    php7.3-cli \
    php7.3-fpm \
    php7.3-common \
    php7.3-curl \
    php7.3-dba \
    php7.3-fpm \
    php7.3-gd \
    php7.3-gmp \
    php7.3-imap \
    php7.3-intl \
    php7.3-ldap \
    php7.3-mbstring \
    php7.3-mysql \
    php7.3-odbc \
    php7.3-pgsql \
    php7.3-recode \
    php7.3-snmp \
    php7.3-soap \
    php7.3-sqlite \
    php7.3-tidy \
    php7.3-xml \
    php7.3-xmlrpc \
    php7.3-xsl \
    php7.3-zip \
    php-gnupg \
    php-imagick \
    php-streams \
    php-fxsl \
    \
    && apt-get -y --quiet purge php5.6* \
    \
    && apt-get -y --quiet purge php7.2* \
    \
    && apt-get -y autoremove \
    \
    && apt-get -y autoclean \
    \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | /usr/bin/php -- --install-dir=/usr/local/bin --filename=composer creates=/usr/local/bin/composer

ADD ssl/* /etc/nginx/ssl/
ADD conf/nginx.conf /etc/nginx/
ADD conf/phpmyadmin.conf /etc/nginx/
ADD conf/symfony.conf /etc/nginx/conf.d/
ADD conf/symfony_dev.conf /etc/nginx/conf.d/

RUN rm -rf /etc/nginx/sites-available
RUN rm -rf /etc/nginx/sites-enabled

RUN \
    sed -i -e 's/max_execution_time = 30/max_execution_time = 300/g' /etc/php/7.3/fpm/php.ini && \
    sed -i -e 's/upload_max_filesize = 2M/upload_max_filesize = 256M/g' /etc/php/7.3/fpm/php.ini && \
    sed -i -e 's/post_max_size = 8M/post_max_size = 512M/g' /etc/php/7.3/fpm/php.ini && \
    sed -i -e 's/memory_limit = 128M/memory_limit = 8G/g' /etc/php/7.3/fpm/php.ini && \
    sed -i -e 's/short_open_tag = Off/short_open_tag = On/g' /etc/php/7.3/fpm/php.ini && \
    sed -i -e 's/short_open_tag = Off/short_open_tag = On/g' /etc/php/7.3/cli/php.ini

WORKDIR /var/www
