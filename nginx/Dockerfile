FROM nginx:latest

ARG UID
ARG GID
RUN usermod -u "$UID" nginx \
    && groupmod -g "$GID" nginx
