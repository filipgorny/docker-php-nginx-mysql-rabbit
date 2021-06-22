FROM php:7.4-fpm-alpine
RUN apk update && \
    apk upgrade && \
    apk add alpine-sdk autoconf bash curl-dev git libxml2-dev linux-headers openssl-dev

RUN apk add libpng libpng-dev icu icu-dev libzip libzip-dev

RUN apk add rabbitmq-c rabbitmq-c-dev git

RUN pecl install amqp

RUN docker-php-ext-enable amqp
RUN docker-php-ext-install curl
RUN docker-php-ext-install sockets
RUN docker-php-ext-install gd
RUN docker-php-ext-install exif
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

RUN docker-php-ext-enable sockets pdo

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN echo "date.timezone = \"Europe/Warsaw\"" >> /usr/local/etc/php/conf.d/timezone.ini

WORKDIR /var/www/app

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["/usr/local/bin/php", "/var/www/app/bin/console", "messenger:consume", "app_bus"]
