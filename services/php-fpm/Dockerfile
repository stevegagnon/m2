FROM php:7.2-fpm

RUN apt-get update \
  && apt-get install -y \
    unzip \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libxslt1-dev \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install pdo_mysql gd bcmath xsl intl soap zip \
  && curl -sS https://getcomposer.org/installer -o composer-setup.php \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && rm composer-setup.php

RUN apt-get purge -y libsodium18

RUN curl https://download.libsodium.org/libsodium/releases/libsodium-1.0.17-stable.tar.gz > sodium.tar.gz \
  && tar -xvf sodium.tar.gz \
  && cd libsodium-stable/ \
  && ./configure \
  && make \
  && make install \
  && cd .. \
  && rm -rf libsodium-stable
