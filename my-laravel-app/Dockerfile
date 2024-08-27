# Usa una imagen base de PHP con Apache
FROM php:7.4-apache

# Instala las dependencias necesarias
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Habilita el módulo de Apache para Laravel
RUN a2enmod rewrite

# Establece el directorio de trabajo en el contenedor
WORKDIR /var/www/html

# Copia el archivo composer.json y composer.lock
COPY composer.json composer.lock ./

# Instala Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Instala las dependencias de la aplicación
RUN composer install --no-scripts --no-autoloader

# Copia el resto del código de la aplicación
COPY . .

# Genera el autoloader
RUN composer dump-autoload --optimize

# Cambia el propietario de los archivos para que Apache pueda acceder a ellos
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Expone el puerto en el que correrá la aplicación
EXPOSE 80