FROM php:7.4-apache

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}/../!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN set -eux \
  && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
  && apt-get update \
  && apt-get install -y \
    zip \
    unzip \
    vim \
    libpq-dev \
  && docker-php-ext-install \
    pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
  && composer config -g repos.packagist composer https://packagist.jp
