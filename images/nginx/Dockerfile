FROM nginx:latest

COPY ./conf/conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY ./conf/includes/magento2.conf /etc/nginx/includes/magento2.conf
COPY ./conf/nginx.conf /etc/nginx/nginx.conf

WORKDIR /var/www/html
