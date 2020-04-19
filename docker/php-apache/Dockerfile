FROM php:7.3-apache

ENV XDEBUG_VERSION 2.9.4
ENV XDEBUG_IDEKEY PHPSTORM
ENV XDEBUG_PORT 10000

WORKDIR /var/www

RUN pecl channel-update pecl.php.net \
    && pecl install "xdebug-${XDEBUG_VERSION}" \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=${XDEBUG_IDEKEY}" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_host=localhost" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=${XDEBUG_PORT}" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_log=/var/log/xdebug.log" >> /usr/local/etc/php/conf.d/xdebug.ini

RUN apt-get update \
    && apt-get install -y git zip libzip-dev unzip \
    && apt-get install -y pkg-config \
    && apt-get install -y libmemcached-dev zlib1g-dev \
    && docker-php-ext-install pdo pdo_mysql mysqli \
    && apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && apt-get install -y libxml2-dev \
    && docker-php-ext-install soap \
    && docker-php-ext-install zip \
    && apt-get install -y libicu-dev \
    && docker-php-ext-install intl \
    && docker-php-ext-install calendar

# Use absolut paths for symbolic link directories, not relative like described here
# https://docs.typo3.org/m/typo3/guide-installation/master/en-us/QuickInstall/GetAndUnpack/Index.html
RUN ln -s /var/www/typo3_src/ /var/www/html/typo3_src \
    && ln -s typo3_src/index.php /var/www/html/index.php \
    && ln -s typo3_src/typo3/ /var/www/html/typo3 \
    && touch html/FIRST_INSTALL

RUN usermod -u 1000 www-data
