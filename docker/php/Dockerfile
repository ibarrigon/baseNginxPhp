FROM php:8.3-fpm

# mismo usuario de nginx para evitar problemas de accesos
RUN adduser -u 1000 --disabled-password --gecos "" appuser

# crear carpeta
RUN mkdir /home/appuser/.ssh
# permisos
RUN chown -R appuser:appuser /home/appuser/

# No solicitar descargar el host key al acceder a nuevos servers
RUN echo "StrictHostKeyChecking no" >> /home/appuser/.ssh/config
# ampliar ancho de columnnas del bash
RUN echo "export COLUMNS=300" >> /home/appuser/.bashrc
# alias de console para ejecutar parametros
RUN echo "alias sf=/appdata/www/bin/console" >> /home/appuser/.bashrc

# copiar la configuracion de php
COPY ./php.ini /usr/local/etc/php/php.ini

# instalar depencias (herramientas necesarias)
RUN apt-get update \
    && apt-get install -y git acl openssl openssh-client wget zip vim libssh-dev \
    && apt-get install -y libpng-dev zlib1g-dev libzip-dev libxml2-dev libicu-dev

RUN docker-php-ext-install gd mysqli 
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip soap bcmath sockets

RUN pecl install xdebug \
    && docker-php-ext-enable --ini-name 05-opcache.ini opcache xdebug

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer self-update
RUN composer clear-cache

# cs-fixer
RUN wget https://cs.symfony.com/download/php-cs-fixer-v2.phar -O php-cs-fixer
RUN chmod a+x php-cs-fixer
RUN mv php-cs-fixer /usr/local/bin/php-cs-fixer

RUN mkdir -p /appdata/www

USER appuser

WORKDIR /appdata/www
