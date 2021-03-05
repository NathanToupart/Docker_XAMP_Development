FROM php:7.4-apache
 
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
 
RUN apt-get update \
    && apt-get install -y --no-install-recommends locales apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev;


RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen
 
RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
   mv composer.phar /usr/local/bin/composer
 
RUN docker-php-ext-configure intl
RUN docker-php-ext-install pdo pdo_mysql gd opcache intl zip calendar dom mbstring zip gd xsl
RUN pecl install apcu && docker-php-ext-enable apcu

RUN apt-get update && apt-get install -y \
    build-essential \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    jpegoptim optipng pngquant gifsicle \
    vim \
    curl \
    ftp \
    openssl

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    ssh \
    libssh2-1 \
    libssh2-1-dev \
    wget \
    libssl-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install ssh2 extension

RUN wget -O libssh2.tar.gz https://www.libssh2.org/download/libssh2-1.9.0.tar.gz \
    && wget -O ssh2.tgz https://pecl.php.net/get/ssh2-1.2.tgz \
    && mkdir libssh2 && tar vxzf libssh2.tar.gz -C libssh2 --strip-components 1 \
    && mkdir ssh2 && tar vxzf ssh2.tgz -C ssh2 --strip-components 1 \
    && cd libssh2 && ./configure \
    && make && make install \
    && cd ../ssh2 && phpize && ./configure --with-ssh2 \
    && make && make install \
    && echo "extension=ssh2.so" >> /usr/local/etc/php/conf.d/ssh2.ini \
    && cd ../ && rm -rf libssh2.tar.gz ssh2.tgz ssh2 libssh2

WORKDIR /var/www/