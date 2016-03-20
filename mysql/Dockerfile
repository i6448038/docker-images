## Github URL: https://github.com/chuantaiyi/docker-images/tree/master/mysql
## Docker URL: https://hub.docker.com/r/chuanty/mysql
##########################################################################
FROM phusion/baseimage:0.9.18

MAINTAINER Liu Yang <yangliu@chuanty.com>
# INSPIRED BY https://github.com/LaraDock/docker-images

ENV DEBIAN_FRONTEND noninteractive
ADD sources.list /etc/apt/sources.list
RUN apt-get update

# Add image configuration and scripts
RUN apt-get install -y mysql-server-5.5
ADD mysql/build/my.cnf /etc/mysql/conf.d/my.cnf
ADD mysql/build/run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

VOLUME ["/var/lib/mysql"]

CMD ["/usr/local/bin/run"]
