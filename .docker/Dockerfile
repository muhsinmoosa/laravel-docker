FROM php:8.4-fpm-alpine

# Install dependencies
RUN apk update && apk add --no-cache \
    git \
    curl \
    libpng-dev \
    jpeg-dev \
    librsvg \
    freetype-dev \
    curl-dev \
    zip \
    unzip \
    bash \
    nginx \
    gmp-dev

# Install intl and requirements    
RUN apk add --no-cache zlib-dev icu-dev g++ && \
docker-php-ext-configure intl && \
docker-php-ext-install intl

# Install mbstring
RUN apk add --no-cache oniguruma-dev && \
docker-php-ext-install mbstring

# Configure GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install pdo_mysql gd bcmath pcntl opcache curl gmp

# Install soap
RUN apk add --no-cache libxml2-dev && \
docker-php-ext-install soap

# Install Redis and MongoDB extensions
RUN apk add --no-cache autoconf build-base openssl-dev && \
    pecl install redis && \
    pecl install mongodb && \
    docker-php-ext-enable redis mongodb && \
    apk del autoconf build-base


RUN rm -rf /tmp/* /var/cache/apk/*

# Copy configuration files.
COPY ./.docker/php/php.ini /usr/local/etc/php/php.ini
COPY ./.docker/nginx/nginx.conf /etc/nginx/nginx.conf

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www

# Copy files from current folder to container current folder (set in workdir).
COPY --chown=www-data:www-data . .

CMD ["sh", "-c", "php-fpm -D && nginx -g 'daemon off;'"]