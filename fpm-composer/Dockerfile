FROM php:fpm-alpine
RUN apk add --update bash \
					vim \
					git \
                    curl \
                    openssh \
		&& rm -rf /var/cache/apk/*

RUN curl -sS https://getcomposer.org/installer -o composer-setup.php && php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

EXPOSE 9000
CMD ["php-fpm"]