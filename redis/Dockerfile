## Github URL: https://github.com/chuantaiyi/docker-images/tree/master/redis
## Docker URL: https://hub.docker.com/r/chuanty/redis
##########################################################################
FROM phusion/baseimage:0.9.18

MAINTAINER Liu Yang <yangliu@chuanty.com>
# INSPIRED BY https://github.com/LaraDock/docker-images

ENV REDIS_USER=redis \
    REDIS_DATA_DIR=/var/lib/redis \
    REDIS_LOG_DIR=/var/log/redis
ADD sources.list /etc/apt/sources.list
RUN add-apt-repository -y ppa:rwky/redis

RUN apt-get update \
 && apt-get install -y redis-server \
 && sed 's/^daemonize yes/daemonize no/' -i /etc/redis/redis.conf \
 && sed 's/^bind 127.0.0.1/bind 0.0.0.0/' -i /etc/redis/redis.conf \
 && sed 's/^# unixsocket /unixsocket /' -i /etc/redis/redis.conf \
 && sed 's/^# unixsocketperm 755/unixsocketperm 777/' -i /etc/redis/redis.conf \
 && sed '/^logfile/d' -i /etc/redis/redis.conf \
 && rm -rf /var/lib/apt/lists/*

COPY redis/build/entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 6379/tcp

VOLUME ["${REDIS_DATA_DIR}"]

ENTRYPOINT ["/sbin/entrypoint.sh"]
