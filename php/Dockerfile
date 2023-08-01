FROM php:7.4-fpm
LABEL author="atif.libra.ali@gmail.com"
WORKDIR /var/app/current

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpng-dev \
    libonig-dev \
    libfreetype6-dev \
    libxext6 \
    libcurl4-openssl-dev \ 
    libxrender1 \
    libfontconfig1 \
    libc-client-dev libkrb5-dev \
    libpng-dev libxpm-dev \ 
    apt-utils \
    zlib1g-dev \
    unzip \
    zip \
    libmagick++-dev \
    libmagickwand-dev \
    libpq-dev \
    libjpeg62-turbo-dev \
    libwebp-dev \ 
    libxpm-dev \
    openssl\
    libssl-dev\
    libgmp-dev\
    libzip-dev \
    locales \
    jpegoptim optipng pngquant gifsicle \
    vim \
    git \
    curl 

    


# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp 
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
        && docker-php-ext-install imap \
        && docker-php-ext-enable imap
RUN docker-php-ext-install gd mysqli pdo_mysql mbstring zip exif pcntl opcache intl pdo_pgsql mysqli json xml curl soap
RUN pecl install imagick-3.4.3 \
redis 
# # Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Clear package lists
RUN apt-get clean && rm -rf /var/lib/apt/lists/*



# # Permissions
# RUN usermod -a -G www-data root
RUN chown -R root:www-data /var/app
RUN chmod 2775 /var/app
RUN find /var/www -type d -exec sudo chmod 2775 {} \;
RUN find /var/www -type f -exec sudo chmod 0664 {} \;
RUN echo "<?php phpinfo(); ?>" > /var/www/webroot/phpinfo.php


# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]