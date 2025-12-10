FROM php:7.4.33-apache

RUN docker-php-source extract \
	&& docker-php-ext-install mysqli \
	&& docker-php-source delete


COPY config/*.load /etc/apache2/mods-enabled/
COPY config/api.conf /etc/apache2/sites-enabled/000-default.conf
COPY config/php.ini /usr/local/etc/php/
COPY config/.htaccess /var/www/openml/.htaccess

RUN mkdir -p /var/www/openml/logs \
    && chown -R www-data:www-data /var/www/openml/logs

RUN mkdir /scripts
COPY set_configuration.sh /scripts/

ENTRYPOINT ["bash", "/scripts/set_configuration.sh"]
