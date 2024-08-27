# Usa una imagen base con PHP 8.2
FROM php:8.2-fpm

# Instala las extensiones necesarias
RUN apt-get update && \
    apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev libzip-dev unzip && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd zip

# Instala Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copia el archivo de configuración de Composer
COPY composer.json /var/www/html/
COPY composer.lock /var/www/html/

# Establece el directorio de trabajo
WORKDIR /var/www/html

# Instala las dependencias de Composer
RUN composer install --no-scripts --no-autoloader

# Copia el código de la aplicación
COPY . /var/www/html/

# Expone el puerto 9000
EXPOSE 9000

# Inicia PHP-FPM
CMD ["php-fpm"]
