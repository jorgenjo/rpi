FROM php:7.1-apache

RUN apt-get update
RUN apt-get install sudo
#RUN apt-get install apt-utils
#RUN apt-get install apache2
#RUN apt-get install php7.0

# Create new web user for apache and grant sudo without password
RUN useradd web -d /var/www -g www-data -s /bin/bash
RUN usermod -aG sudo web
RUN echo 'web ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Add sudo to www-data
RUN echo 'www-data ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

RUN a2enmod rewrite expires && service apache2 restart

# Our apache volume
VOLUME /var/www/html

COPY /index.php /var/www/html
COPY /phpinfo.php /var/www/html

# create directory for ssh keys
RUN mkdir /var/www/.ssh/
RUN chown -R web:www-data /var/www/
RUN chmod -R 600 /var/www/.ssh/


# Set timezone to Europe/Paris
RUN echo "Europe/Paris" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata


EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
