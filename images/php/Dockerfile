FROM phpdockerio/php73-fpm:latest

ARG app_path
ENV APP_PATH=$app_path

ARG username
ENV USERNAME=$username

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

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

#set folder owner for composer cache
RUN mkdir -p $APP_PATH && ls $APP_PATH
RUN useradd -m $USERNAME
RUN chown -R $USERNAME:$USERNAME $APP_PATH

# Make sure the volume mount point is empty
RUN rm -rf $APP_PATH/*
