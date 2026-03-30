FROM php:7.4-apache

# Install dependencies
RUN apt-get update \
  && apt-get install -y \
  # dependency for zip
    libzip-dev

RUN apt-get update \
  && apt-get install -y \
  # dependency for zip
    libssh2-1-dev \
    libssh2-1

#Install mysqli
RUN docker-php-ext-install mysqli \
    zip

RUN docker-php-ext-enable mysqli

#Install xdebug
RUN pecl install xdebug-2.9.8 \
    && docker-php-ext-enable xdebug

RUN pecl install pcov \
    && docker-php-ext-enable pcov

RUN pecl install ssh2 \
    && docker-php-ext-enable ssh2

RUN apt-get update && apt-get install -y vim nano

# Install unzip
RUN apt-get update && apt-get install -y unzip

RUN apt-get update && apt-get install -y default-mysql-client

RUN apt-get update && apt-get install -y \
    libpq-dev \
    && docker-php-ext-install pgsql pdo_pgsql

RUN apt-get update && apt-get install -y \
    t1utils \
    libfreetype6-dev \
    fontconfig \
    fonts-freefont-ttf

RUN mkdir -p /usr/share/fonts/custom

RUN fc-cache -fv

RUN apt install locate

RUN apt-get update && apt-get install -y wget build-essential libpcre3-dev

ADD conf.d/xdebug.ini $PHP_INI_DIR/conf.d/zz-xdebug.ini
ADD conf.d/error_xdebug.ini $PHP_INI_DIR/conf.d/error_xdebug.ini
ADD conf.d/error_reporting.ini $PHP_INI_DIR/conf.d/error_reporting.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN groupadd -g 1000 myuser && \
    useradd -u 1000 -g 1000 -s /bin/bash -m myuser && \
    usermod -aG sudo myuser && \
    echo 'myuser:mypass' | chpasswd

USER myuser
