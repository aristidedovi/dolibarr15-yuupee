FROM php:7.4-apache
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN apt-get update && apt-get upgrade -y
RUN rm -rf /var/www/html/htdocs/conf/conf.php && touch /var/www/html/htdocs/conf/conf.php && chmod 777 /var/www/html/htdocs/conf/conf.php
