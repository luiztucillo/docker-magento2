FROM nginx:latest

ARG app_path
ENV APP_PATH=$app_path

ARG username
ENV USERNAME=$username

#set folder owner for composer cache
RUN mkdir -p $APP_PATH && ls $APP_PATH
RUN useradd -m $USERNAME
RUN chown -R $USERNAME:$USERNAME $APP_PATH

# Make sure the volume mount point is empty
RUN rm -rf $APP_PATH/*
