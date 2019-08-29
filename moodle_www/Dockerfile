FROM php:7.3-apache

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y \
    vim \
    libzip-dev \
    zip \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip \
    && docker-php-ext-install mysqli 
#Dependencias de php-intl
RUN apt-get install -y zlib1g-dev libicu-dev g++
RUN docker-php-ext-install intl
#Dependencias de php-gd
RUN apt-get install -y libpng-dev
RUN docker-php-ext-install gd
#Dependencias de php-xmlrpc y php-soap
RUN apt-get install libxml2-dev
RUN docker-php-ext-install xmlrpc
RUN docker-php-ext-install soap
# Instalar y habilitar php-OPCache
RUN docker-php-ext-install opcache && \
    docker-php-ext-enable opcache



RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY ./config/opcache.ini $PHP_INI_DIR/conf.d/

RUN addgroup --gid 1201 gmoodle

RUN mkdir /var/moodledata
RUN chown -R www-data:gmoodle /var/moodledata
RUN chmod -R 775 /var/moodledata
RUN chmod -R g+s /var/moodledata

# Copiado de archivos para pruebas...
# Esta linea se mantiene comentada para crear IMAGEN
# COPY ./www/ /var/www/html/
