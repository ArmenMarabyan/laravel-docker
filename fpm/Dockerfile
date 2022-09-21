FROM php:8-fpm

RUN apt-get update \
  && apt-get install -y \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libxslt1-dev \
    libzip-dev \
    libonig-dev \
    git \
    curl \
    unzip \
    libwebp-dev \
    libpng-dev libxpm-dev


RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev

RUN docker-php-ext-install mbstring

RUN apt-get install -y libzip-dev
RUN docker-php-ext-install zip

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-webp=/usr/include/  --with-jpeg=/usr/include/

RUN docker-php-ext-install gd



RUN curl -sS https://getcomposer.org/installer -o composer-setup.php

RUN php composer-setup.php \
    --install-dir=/usr/local/bin \
    --filename=composer

RUN rm composer-setup.php

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory contents
COPY . /var/www/html

# Copy existing application directory permissions
COPY --chown=www:www . /var/www/html

RUN whoami

# Change current user to www
USER www
RUN whoami

WORKDIR /var/www/html
