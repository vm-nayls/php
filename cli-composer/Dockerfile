FROM php:alpine
ARG VCS_REF
LABEL org.label-schema.vcs-ref=$VCS_REF \
	  org.label-schema.vcs-url="https://github.com/vm-nayls/php"

RUN apk add --update bash vim git curl openssh && \
	rm -rf /var/cache/apk/*

RUN curl -sS https://getcomposer.org/installer -o composer-setup.php && php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

CMD ["php", "-a"]