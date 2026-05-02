FROM php:7.4-fpm

COPY php.ini /usr/local/etc/php/

# install packages + node in one layer
RUN apt-get update && apt-get install -y \
    vim \
    zlib1g-dev \
    git \
    libzip-dev \
    libonig-dev \
    libc-client-dev \
    libkrb5-dev \
    curl \
    gnupg \
    && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

# php extensions
RUN PHP_OPENSSL=yes docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install zip pdo_mysql mysqli mbstring imap

# composer
COPY --from=composer /usr/bin/composer /usr/bin/composer