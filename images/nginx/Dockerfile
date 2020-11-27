FROM nginx:latest

RUN useradd -m ltucillo
RUN usermod -aG sudo ltucillo
RUN mkdir -p /var/www/html
RUN chown -R ltucillo: /var/www/html

COPY ./conf/conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY ./conf/includes/magento2.conf /etc/nginx/includes/magento2.conf
COPY ./conf/nginx.conf /etc/nginx/nginx.conf

WORKDIR /var/www/html
