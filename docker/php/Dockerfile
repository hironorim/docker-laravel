FROM php:7.4.5-fpm

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1

RUN docker-php-ext-install bcmath pdo_mysql opcache && pecl install xdebug && docker-php-ext-enable xdebug && apt-get update && apt-get install -y git unzip

COPY --from=composer /usr/bin/composer /usr/bin/composer
