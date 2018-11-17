# Build backend source

FROM composer:1.7 as vendor

WORKDIR /app

COPY composer.json composer.lock /app/

RUN composer install  \
    --ignore-platform-reqs \
    --no-ansi \
    --no-autoloader \
    --no-dev \
    --no-interaction \
    --no-scripts

COPY . /app/

RUN composer dump-autoload --optimize --classmap-authoritative


# Build frontend assets

FROM node:8.11 as frontend

WORKDIR /app

COPY package.json yarn.lock webpack.mix.js /app/
COPY resources/js/ /app/resources/js/
COPY resources/sass/ /app/resources/sass/

RUN yarn && yarn production


# Application

FROM php:7.2-apache

RUN a2enmod rewrite

ADD .docker/apache.conf /etc/apache2/sites-available/000-default.conf
RUN mv $PHP_INI_DIR/php.ini-production $PHP_INI_DIR/php.ini
ADD .docker/php.ini ${PHP_INI_DIR}/conf.d/99-overrides.ini

WORKDIR /app
COPY --from=vendor /app /app
COPY --from=frontend /app/public /app/public
RUN chown -R www-data:www-data /app/storage /app/bootstrap/cache
