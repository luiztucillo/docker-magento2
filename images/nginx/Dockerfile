FROM nginx:latest

ARG app_path
ENV APP_PATH=$app_path

ARG username
ENV USERNAME=$username

#set folder owner for composer cache
RUN mkdir -p $APP_PATH && ls $APP_PATH
RUN useradd -m $USERNAME
RUN chown -R $USERNAME:$USERNAME $APP_PATH

COPY ./conf/conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY ./conf/includes/magento2.conf /etc/nginx/includes/magento2.conf
COPY ./conf/nginx.conf /etc/nginx/nginx.conf

# Make sure the volume mount point is empty
RUN rm -rf $APP_PATH/*
