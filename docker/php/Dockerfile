FROM php:7.2-fpm

COPY php.ini /usr/local/etc/php/

RUN apt-get update

#pdo
RUN apt-get update \
  && apt-get install -y zlib1g-dev mariadb-client \
  && docker-php-ext-install zip pdo_mysql

#node
RUN apt-get install -y wget git unzip libpq-dev \
    && : 'Install Node.js' \
    &&  curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && : 'Install PHP Extensions' \
    && apt-get install -y nodejs

#composer
COPY --from=composer /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

#git
RUN apt-get install -y git

# phpredis
RUN git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis
RUN docker-php-ext-install redis

#vim
RUN apt-get install -y vim

#workdir
WORKDIR /var/www

RUN composer global require "laravel/installer"
