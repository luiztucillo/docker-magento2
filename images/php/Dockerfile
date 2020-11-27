FROM phpdockerio/php73-fpm:latest

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN useradd -d /home/ltucillo -ms /bin/bash -g root -G sudo -p ltucillo ltucillo
RUN mkdir -p /var/www/html
RUN chown -R ltucillo: /var/www/html

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        php-memcached \
        php7.3-mysql \
        php-redis \
        php-xdebug \
        php7.3-bcmath \
        php7.3-gd \
        php7.3-intl \
        php7.3-soap \
        git \
        golang-go \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

#MAILHOG
RUN mkdir gocode && echo "export GOPATH=$HOME/gocode" >> ~/.profile && source ~/.profile
RUN go get github.com/mailhog/MailHog && go get github.com/mailhog/mhsendmail
RUN cp ~/gocode/bin/MailHog /usr/local/bin/mailhog && cp ~/gocode/bin/mhsendmail /usr/local/bin/mhsendmail

#CONFIGURE
COPY php.ini /etc/php/7.3/fpm/php.ini
COPY php-fpm.conf /etc/php/7.3/fpm/

#COMPOSER
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && rm composer-setup.php \
    && mv composer.phar /usr/bin/composer \
    && chmod +x /usr/bin;composer

USER ltucillo
WORKDIR /var/www/html