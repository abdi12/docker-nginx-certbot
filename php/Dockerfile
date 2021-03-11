FROM php:7.3-fpm-alpine

WORKDIR /var/www/html

# create a user with ID is aqual to user on host then join ti group www-data in php-fpm
RUN adduser -u 1000 -D www -G www-data

RUN apk add --update --no-cache gcc make g++ autoconf libgd libpng-dev libjpeg-turbo-dev freetype-dev bzip2-dev \
    libzip-dev libxml2-dev libmcrypt-dev libmcrypt gettext-dev gmp-dev libxslt-dev \
    && pecl install mcrypt-1.0.2 && docker-php-ext-enable mcrypt

RUN docker-php-ext-install -j$(nproc) iconv gd pdo pdo_mysql opcache bcmath bz2 mysqli xmlrpc \
    calendar gettext zip sysvmsg sysvsem sysvshm exif hash pcntl soap wddx sockets gmp hash xsl shmop && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY laravel ./

COPY --chown=www:www-data laravel /var/www/html

USER www

EXPOSE 9000