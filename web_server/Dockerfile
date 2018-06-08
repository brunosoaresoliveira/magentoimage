From ubuntu:18.04

MAINTAINER Bruno Soares <bruno.soares.oliveira@gmail.com>

#Update packages list and install apache2
RUN apt-get -qq update \
		&& apt-get -qq -y install apache2

#Add PHP repository
RUN apt-get -qq update \
		&& apt-get -qq -y install software-properties-common \
		&& add-apt-repository -y ppa:ondrej/php

#Install php 7.1
RUN apt-get -qq update \
		&& export RUN DEBIAN_FRONTEND=noninteractive && apt-get install -y php7.1

#Install required PHP components for Magento 2
RUN apt-get -qq update \
		&& apt-get -qq -y install libapache2-mod-php7.1 php7.1-common php7.1-mbstring php7.1-xmlrpc php7.1-soap php7.1-gd php7.1-xml php7.1-intl php7.1-mysql php7.1-cli php7.1-zip php7.1-curl php7.1-mcrypt php7.1-bcmath

#RUN sed -i -e"s/^memory_limit\s*=\s*128M/memory_limit = 256M/" /etc/php/7.0/apache2/php.ini

RUN a2enmod php7.1 \
		&& a2enmod rewrite \
		&& a2enmod headers

#Remove default virtual host config and default php files from Apache folder.
RUN rm /etc/apache2/sites-enabled/000-default.conf /var/www/html/*

CMD ["/usr/sbin/apache2ctl","-D","FOREGROUND"]
