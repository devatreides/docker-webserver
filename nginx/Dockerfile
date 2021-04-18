FROM nginx:1.19.0-alpine

LABEL maintainer="Tom Benevides"

# ARG DOMAINS
# ENV DOMAINS ${DOMAINS}
# ARG DOMAINS_REDIRECT
# ENV DOMAINS_REDIRECT ${DOMAINS_REDIRECT}
# ARG PHP_FPM_UPSTREAM_PORT
# ENV PHP_FPM_UPSTREAM_PORT ${PHP_FPM_UPSTREAM_PORT}
# ARG NGINX_SSL_HOST_PATH
# ENV NGINX_SSL_HOST_PATH ${NGINX_SSL_HOST_PATH}

RUN apk update \
    && apk upgrade \
    && apk add --no-cache shadow \
    && apk add --no-cache openssl \
    && apk add --no-cache bash \
    && apk add --no-cache nano

COPY config/nginx.conf /etc/nginx/
# COPY config/sites/*.conf /etc/nginx/sites-available/
RUN rm /etc/nginx/conf.d/default.conf

RUN set -x ; \
    addgroup -g 82 -S www-data ; \
    adduser -u 82 -D -S -G www-data www-data ;

EXPOSE 80

ADD ./startup.sh /opt/startup.sh
RUN sed -i 's/\r//g' /opt/startup.sh
CMD ["/bin/bash", "/opt/startup.sh"]
