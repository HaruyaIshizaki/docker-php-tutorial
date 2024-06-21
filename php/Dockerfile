FROM php:8.1-fpm-alpine

# https://hub.docker.com/_/php#:~:text=ext%2Dconfigure%2C-,docker%2Dphp%2Dext%2Dinstall,-%2C%20and%20docker%2Dphp
RUN docker-php-ext-install pdo pdo_mysql

# Set environment variable for Composer
ENV COMPOSER_ALLOW_SUPERUSER=1

COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

COPY ./app/composer.* ./

RUN composer install \
    --prefer-dist \
    --no-dev \
    --no-scripts \
    --no-progress \
    --no-interaction

COPY ./app .

RUN composer dump-autoload --optimize