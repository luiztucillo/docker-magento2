FROM phpdockerio/php73-fpm:latest

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN useradd -m ltucillo
RUN usermod -aG sudo ltucillo
USER ltucillo

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php-memcached php7.3-mysql php-redis php-xdebug php7.3-bcmath php7.3-gd php7.3-intl php7.3-soap \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

#CONFIGURE
COPY php.ini /etc/php/7.3/fpm/php.ini
COPY php-fpm.conf /etc/php/7.3/fpm/

#COMPOSER
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && rm composer-setup.php \
    && mv composer.phar /usr/bin/composer;
