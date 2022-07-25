FROM php:8.1.8-fpm

RUN apt-get update && apt-get install -y \
    zip \
    unzip \
    curl \
    git \
    vim

# # # Composer
COPY --from=composer /usr/bin/composer /usr/local/bin/composer

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions \
    pdo_pgsql

RUN apt-get clean

WORKDIR /srv/www/

COPY ./storage /var/www/storage
COPY ./bootstrap/cache /var/www/bootstrap/cache


RUN chown -R www-data:www-data /var/www && \
    chmod -R 755 /var/www && \
    useradd -m docker && echo "docker:docker" | chpasswd && \
    adduser docker sudo

USER docker

CMD ["php-fpm"]
