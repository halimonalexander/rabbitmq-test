FROM php:7.4-fpm
USER root

MAINTAINER eAuth <admin@eauth.cc>

# Arguments defined in docker-compose.yml
ARG user
ARG uid
ARG port

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
 && docker-php-ext-install exif iconv mbstring pdo pdo_mysql pcntl zip \
 # Install composer
 && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
 # Add user for laravel application
 && groupadd -g $uid $user \
 && useradd -u $uid -ms /bin/bash -g www $user

# Copy existing application directory permissions
#COPY --chown=$user:www . /var/www

# Set working directory
WORKDIR /var/www

# Change current user to www
USER $user

# Expose port $port and start php-fpm server
EXPOSE $port
CMD ["php-fpm"]
