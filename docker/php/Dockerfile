FROM php:7.4.9-fpm

COPY php.ini /usr/local/etc/php/

RUN apt update \
    && apt install -y default-mysql-client zlib1g-dev libzip-dev unzip \
    && docker-php-ext-install pdo_mysql zip

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update

# あなたのUID/GIDを使ってユーザーを作成
ARG UID=1000
ARG GID=1000

RUN groupadd -g ${GID} appgroup && \
    useradd -u ${UID} -g ${GID} -m appuser && \
    chown -R appuser:appgroup /var/www

WORKDIR /var/www
USER appuser
