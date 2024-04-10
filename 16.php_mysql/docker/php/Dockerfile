FROM php:8.1-apache


# install mysql extension
RUN apt update && \
    docker-php-ext-install mysqli pdo pdo_mysql && \
    apt clean
