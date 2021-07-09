FROM php:5.4-apache

ARG TZ

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}/../!g' /etc/apache2/apache2.conf

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

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
