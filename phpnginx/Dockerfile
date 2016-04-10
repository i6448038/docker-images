## Github URL: https://github.com/chuantaiyi/docker-images/tree/master/phpnginx
## Docker URL: https://hub.docker.com/r/chuanty/phpnginx
#############################################################################
FROM phusion/baseimage:0.9.18

MAINTAINER Liu Yang <yangliu@chuanty.com>
# INSPIRED BY https://github.com/LaraDock/docker-images

# Default baseimage settings
ENV HOME /root
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
CMD ["/sbin/my_init"]
ENV DEBIAN_FRONTEND noninteractive

ADD sources.list /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y --force-yes software-properties-common
RUN apt-get install -y language-pack-en-base
RUN LC_ALL=en_US.UTF-8 apt-add-repository ppa:fkrull/deadsnakes-python2.7 -y
RUN LC_ALL=en_US.UTF-8 apt-add-repository ppa:nginx/development -y
RUN LC_ALL=en_US.UTF-8 apt-add-repository ppa:chris-lea/redis-server -y
RUN LC_ALL=en_US.UTF-8 apt-add-repository ppa:ondrej/apache2 -y
RUN LC_ALL=en_US.UTF-8 apt-add-repository ppa:ondrej/php -y

RUN apt-get update && \
    apt-get install -y --force-yes nginx \
    php7.0-fpm php7.0-cli php7.0-dev php7.0-mysql php7.0-mcrypt \
    php7.0-curl php7.0-gd php7.0-intl php7.0-zip php7.0-imap php7.0-xml php7.0-mbstring php-imagick && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
           /tmp/* \
           /var/tmp/*

 # Set The Timezone

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# Configure nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN sed -i "s/sendfile on/sendfile off/" /etc/nginx/nginx.conf
RUN mkdir -p /var/www
RUN mkdir -p /var/run/php

# Configure PHP
RUN sed -i "s/error_reporting = .*/error_reporting = E_ALL/" /etc/php/7.0/cli/php.ini
RUN sed -i "s/display_errors = .*/display_errors = On/" /etc/php/7.0/cli/php.ini
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.0/cli/php.ini
RUN sed -i "s/memory_limit = .*/memory_limit = 512M/" /etc/php/7.0/cli/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = Asia\/Shanghai/" /etc/php/7.0/cli/php.ini

RUN sed -i "s/error_reporting = .*/error_reporting = E_ALL/" /etc/php/7.0/fpm/php.ini
RUN sed -i "s/display_errors = .*/display_errors = On/" /etc/php/7.0/fpm/php.ini
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.0/fpm/php.ini
RUN sed -i "s/memory_limit = .*/memory_limit = 512M/" /etc/php/7.0/fpm/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = Asia\/Shanghai/" /etc/php/7.0/fpm/php.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.0/fpm/php-fpm.conf
RUN sed -i "s/;pid = \/run\/php\/php7.0-fpm.pid/pid = \/var\/run\/php\/php7.0-fpm.pid/" /etc/php/7.0/fpm/php-fpm.conf

RUN phpenmod mcrypt

# Add nginx service
RUN mkdir /etc/service/nginx
ADD phpnginx/build/nginx/run.sh /etc/service/nginx/run
RUN chmod +x /etc/service/nginx/run

# Add PHP service
RUN mkdir /etc/service/phpfpm
ADD phpnginx/build/php/run.sh /etc/service/phpfpm/run
RUN chmod +x /etc/service/phpfpm/run

VOLUME ["/var/www", "/etc/nginx/sites-available", "/etc/nginx/sites-enabled"]

WORKDIR /var/www

EXPOSE 80
