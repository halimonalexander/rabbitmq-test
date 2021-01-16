FROM php:7.4-fpm

# Install dependencies
RUN apt-get update \
 && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    unzip \
 # Clear cache
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 # Install extensions
 && docker-php-ext-install exif iconv mbstring pdo pdo_mysql pcntl zip

 ADD ./docker/php/php.ini /usr/local/etc/php/php.ini

 # Install composer
 RUN curl -sS https://getcomposer.org/installer \
     | php -- --install-dir=/usr/local/bin --filename=composer --quiet

# Set working directory
WORKDIR /var/www

CMD ["php-fpm"]
