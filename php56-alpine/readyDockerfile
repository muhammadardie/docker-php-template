FROM php:5.6-apache

# RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y update \
    && apt-get install -y --no-install-recommends \
    apt-utils \
    apache2-utils \
    git \
    nano \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

# Install PHP Extensions
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions gd xdebug pdo pdo_pgsql mcrypt zip soap mbstring json mysql intl curl xml

# Install composer for PHP dependencies
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Enable Apache mod_rewrite
RUN a2enmod rewrite ssl headers

RUN chown -R www-data:www-data /var/www

EXPOSE 80
EXPOSE 443
