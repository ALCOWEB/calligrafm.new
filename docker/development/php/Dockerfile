FROM php:7.4-fpm

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        nginx \
        postgresql-client \
        libpq-dev \
        git \
        zip \
        unzip && \
    docker-php-ext-install pdo_pgsql && \
    pecl install xdebug-2.9.8 && \
    docker-php-ext-enable xdebug

WORKDIR /app
COPY . /app

# Настраиваем PHP
RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-error-reporting.ini && \
    echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-error-reporting.ini && \
    echo "log_errors = On" >> /usr/local/etc/php/conf.d/docker-php-error-reporting.ini && \
    echo "date.timezone = UTC" >> /usr/local/etc/php/conf.d/docker-php-timezone.ini

# Устанавливаем composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer
