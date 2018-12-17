FROM php:7.1-cli-alpine
ARG VCS_REF
LABEL org.label-schema.vcs-ref=$VCS_REF \
	  org.label-schema.vcs-url="https://github.com/vm-nayls/php"

RUN apk add --update bash vim git curl openssh && \
	rm -rf /var/cache/apk/*


RUN echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
 && echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "$PHP_INI_DIR/conf.d/date_timezone.ini"

RUN apk add --no-cache --virtual .build-deps zlib-dev \
 && docker-php-ext-install zip \
 && runDeps="$( \
    scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
    | tr ',' '\n' \
    | sort -u \
    | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )" \
 && apk add --virtual .composer-phpext-rundeps $runDeps \
 && apk del .build-deps


RUN curl -sS https://getcomposer.org/installer -o composer-setup.php && php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

CMD ["php", "-a"]