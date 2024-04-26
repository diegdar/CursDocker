FROM php:8.1-apache as dev
# install mysql extension
RUN apt update && \
    docker-php-ext-install mysqli pdo pdo_mysql && \
    apt clean

FROM dev as prod
ADD /code/ /var/www/html/