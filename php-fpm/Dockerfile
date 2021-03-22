FROM phpdockerio/php74-fpm:latest
WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install git golang-go php7.4-memcached php7.4-mysql php7.4-redis php7.4-bcmath php7.4-gd php7.4-intl php7.4-soap \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

### Install sendmail for use with mailhog
ENV GOPATH /tmp
RUN cd /tmp \
    && go get github.com/mailhog/mhsendmail \
    && cd /tmp/src/github.com/mailhog/mhsendmail/ \
    && go build \
    && cp /tmp/src/github.com/mailhog/mhsendmail/mhsendmail /usr/local/bin