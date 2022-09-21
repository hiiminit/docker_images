FROM php:7.0.33-apache

COPY config/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY config/php.ini /usr/local/etc/php/php.ini

RUN a2enmod vhost_alias

# PHP extensions
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && \
    docker-php-ext-configure mysqli --with-mysqli=mysqlnd && \
    docker-php-ext-install pdo_mysql
