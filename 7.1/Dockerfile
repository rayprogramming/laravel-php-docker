FROM php:7.1-apache-stretch
MAINTAINER Lucas Pearson <pearson.lucas@gmail.com>

RUN apt-get update && apt-get -y install git curl unzip supervisor nodejs libmcrypt-dev libreadline-dev libxml2 libxml2-dev libwebp-dev libjpeg62-turbo-dev libpng-dev libxpm-dev libfreetype6-dev && apt-get -y autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mcrypt xml gd zip mbstring json
RUN /usr/sbin/a2enmod rewrite

ADD 000-laravel.conf /etc/apache2/sites-available/
ADD 001-laravel-ssl.conf /etc/apache2/sites-available/
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN /usr/sbin/a2dissite '*' && /usr/sbin/a2ensite 000-laravel 001-laravel-ssl
RUN /usr/sbin/a2enmod ssl

RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data
RUN /usr/bin/curl -sS https://getcomposer.org/installer |/usr/local/bin/php
RUN /bin/mv composer.phar /usr/local/bin/composer
RUN /bin/chown www-data:www-data -R /var/www

WORKDIR /var/www

EXPOSE 80
EXPOSE 443

CMD ["/usr/bin/supervisord"]
