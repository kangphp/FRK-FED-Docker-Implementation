# Dockerfile untuk Lumen
FROM php:8.2-apache

# Install dependencies
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    git \
    openssl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

# Enable Apache Rewrite Module
RUN a2enmod rewrite

# Set working directory to /var/www/html
WORKDIR /var/www/html

# Copy Lumen service files
RUN git clone https://github.com/kangphp/FRK-FED-Authentication-Service.git  /tmp/repo \
    && cp -r /tmp/repo/* . \
    && rm -rf /tmp/repo

# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install PHP dependencies
RUN composer install

# Set permissions
RUN chown -R www-data:www-data /var/www \
    && chmod -R 755 /var/www


# Expose port
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]
