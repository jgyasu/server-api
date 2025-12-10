FROM php:7.4.33-apache

# Install mysqli extension
RUN docker-php-source extract \
    && docker-php-ext-install mysqli \
    && docker-php-source delete

# Configuration files from the host's server-api/docker/php/config directory.
COPY config/*.load /etc/apache2/mods-enabled/
COPY config/api.conf /etc/apache2/sites-enabled/000-default.conf
COPY config/php.ini /usr/local/etc/php/

# .htaccess should be copied to the mounted directory.
# Note: Ensure the OpenML repository already contains an index.php at its root
# if the Apache configuration expects it there.
COPY config/.htaccess /var/www/openml/.htaccess

# --- IMPORTANT ADDITION FOR LOGS AND PERMISSIONS ---
# Create logs directory *inside* the mounted volume structure and set permissions.
# The logs directory should be empty or non-existent in the host's OpenML repo.
RUN mkdir -p /var/www/openml/logs \
    && chown -R www-data:www-data /var/www/openml/logs

RUN mkdir /scripts
COPY set_configuration.sh /scripts/

ENTRYPOINT ["bash", "/scripts/set_configuration.sh"]
