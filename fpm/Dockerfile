FROM php:7.1.18-fpm

RUN truncate -s 0 /etc/apt/sources.list
RUN echo "deb http://mirrors.digitalocean.com/debian/ jessie main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.digitalocean.com/debian/ jessie-updates main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.digitalocean.com/debian/ jessie-backports main" >> /etc/apt/sources.list

RUN apt-get update --fix-missing && apt-get upgrade -y && apt-get install -y --allow-downgrades git \
    mc unzip \
    libmcrypt-dev libssl-dev \
    libpng-dev libjpeg-dev libfreetype6-dev \
    zlib1g=1:1.2.8.dfsg-2+b1 zlib1g-dev

# install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# set timezone to WIB
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql mcrypt gettext zip
# Install the PHP gd library
RUN docker-php-ext-install gd && \
    docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd

WORKDIR /var/www
