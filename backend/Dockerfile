# prestage build used for handling composer
FROM composer:1.7 as vendor

COPY composer.json composer.json
COPY composer.lock composer.lock

RUN composer install \
    --ignore-platform-reqs \
    --no-interaction \
    --no-plugins \
    --no-scripts \
    --prefer-dist

# main build stage


FROM richarvey/nginx-php-fpm
RUN rm /var/www/html/index.php
RUN mkdir /var/www/php
RUN mkdir /var/www/vendor
COPY php /var/www/php
COPY --from=vendor /app/vendor/ /var/www/vendor/
COPY public_html /var/www/html
EXPOSE 80