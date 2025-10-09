# --- Dockerfile (app/Dockerfile) ---

# Menggunakan image resmi PHP 8.3 (sesuaikan dengan versi PHP Laravel 12)
# Kami menggunakan image 'fpm-alpine' yang ringan dan cocok untuk produksi/pengembangan
FROM php:8.3-fpm-alpine

# Argument untuk versi Node.js yang akan diinstal
ARG NODE_VERSION=20

# Instal dependensi sistem, termasuk yang dibutuhkan oleh PHP dan Node.js
RUN apk update && apk add --no-cache \
    libzip-dev \
    libpng-dev \
    jpeg-dev \
    mariadb-client \
    nodejs-current \
    npm \
    git \
    unzip \
    bash \
    && rm -rf /var/cache/apk/*

# Instal ekstensi PHP yang umum digunakan oleh Laravel
RUN docker-php-ext-install pdo pdo_mysql zip exif pcntl \
    && docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install gd

# Instal Composer secara global
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Atur direktori kerja
WORKDIR /var/www/html

# Ekspos port FPM
EXPOSE 9000

# Pengaturan hak akses (opsional, tergantung pada kebutuhan keamanan dan user host)
# Biasanya, dalam pengembangan, kita akan menggunakan user www-data
# RUN chown -R www-data:www-data /var/www/html

# Perintah startup
CMD ["php-fpm"]
