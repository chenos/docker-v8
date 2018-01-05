# Dockerfile

```Dockerfile
FROM php:7.0-fpm

RUN apt-get update
RUN apt-get install -y --no-install-recommends git

RUN git clone https://github.com/chenos/v8.git /opt/v8
RUN git clone https://github.com/phpv8/v8js.git /tmp/v8js

RUN cd /opt/v8 && git checkout tags/v6.1.99
RUN cd /tmp/v8js && git checkout tags/2.0.0

RUN cd /tmp/v8js && phpize
RUN cd /tmp/v8js && ./configure --with-v8js=/opt/v8
RUN cd /tmp/v8js && make
RUN cd /tmp/v8js && make test
RUN cd /tmp/v8js && make install
RUN docker-php-ext-enable v8js

```
