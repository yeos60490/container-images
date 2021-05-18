FROM php:7.3-apache

RUN apt-get -y update; \
        apt-get -y install vim; \
        apt-get -y install git;

RUN rm /etc/apt/preferences.d/no-debian-php; \
        apt-get -y install php7.3-mysql;
