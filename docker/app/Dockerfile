FROM php:7.4-apache

RUN apt-get update && apt-get install -y \
      apt-utils \
      libpq-dev \
      libpng-dev \
      libzip-dev \
      libfreetype6-dev \
      zip unzip \
      git && \
      docker-php-ext-install pdo_mysql && \
      docker-php-ext-install mysqli && \
      docker-php-ext-enable  mysqli && \
      docker-php-ext-install bcmath && \
      docker-php-ext-install gd && \
      docker-php-ext-install zip && \
      apt-get clean && \
      rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ \
      && docker-php-ext-install gd
RUN docker-php-ext-install gd && \
      docker-php-ext-enable  gd
RUN mkdir -p /home/root/tmp

COPY ./docker/app/php.ini /usr/local/etc/php/conf.d/php.ini

WORKDIR /var/www/html
# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
      --filename=composer \
      --install-dir=/usr/local/bin \