FROM resin/rpi-raspbian:jessie-20161207

# To install php7.0we need the testing branch of raspbian

RUN echo "deb http://mirrordirector.raspbian.org/raspbian/ stretch main contrib non-free rpi" > /etc/apt/sources.list.d/raspbian_nonfree.list
#RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" > /etc/apt/sources.list.d/php7.list
#RUN echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main " >> /etc/apt/sources.list.d/php7.list

#RUN gpg --keyserver keyserver.ubuntu.com --recv E5267A6C && gpg --export --armor E5267A6C | apt-key add -

RUN apt-get update
RUN apt-get install -y php7.0
RUN apt-get install -y php7.0-fpm
RUN apt-get install -y php7.0-curl
RUN apt-get install -y php7.0-sqlite3
RUN apt-get install -y php7.0-json
RUN apt-get install -y php7.0-cli
RUN apt-get install -y php7.0-intl
RUN apt-get install -y php7.0-mcrypt
RUN apt-get install -y php7.0-xmlrpc
RUN apt-get install -y php7.0-pgsql
RUN apt-get install -y php7.0-common
RUN apt-get install -y php7.0-xml
RUN apt-get install -y php7.0-zip
RUN apt-get install -y php7.0-mbstring
RUN apt-get install -y php7.0-opcache
RUN apt-get install -y php7.0-mysqli
RUN apt-get install -y php7.0-gd

RUN sed -Ei 's/^listen.*/listen = 9000/' /etc/php/7.0/fpm/pool.d/www.conf

RUN mkdir /run/php/
RUN service php7.0-fpm stop

EXPOSE 9000

CMD ["php-fpm7.0", "-F"]
