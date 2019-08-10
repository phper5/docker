FROM ubuntu:18.04
ENV UPDATE_AT 20171205
RUN apt-get update &&\
 apt-get install -y build-essential &&\
 apt-get install -y wget
RUN apt-get install -y imagemagick libmagick++-dev
#准备环境
#####################libxml2
RUN apt-get install -y libxml2-dev openssl  libssl-dev
#####################OpenSSL
RUN mkdir -p /usr/local/openssl/include/openssl/
RUN ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h
RUN mkdir -p /usr/local/openssl/lib/
RUN ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a
RUN ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/
#####################curl
RUN apt-get install  -y curl 
RUN apt-get install -y libcurl4 libcurl4-openssl-dev
RUN mkdir -p /usr/local/curl/7.48.0 && ln -s /usr/include/x86_64-linux-gnu/curl /usr/local/curl/7.48.0/curl
##################### iconv library
WORKDIR /source/
RUN wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz
RUN tar -xvf libiconv-1.15.tar.gz
WORKDIR /source/libiconv-1.15
RUN ./configure
RUN make && make install
#####################libmcrypt
RUN apt-get install -y libmcrypt-dev
#####################libedit
RUN apt-get install  -y libedit-dev

RUN mkdir -p /source/php 
WORKDIR /source
RUN wget https://www.php.net/distributions/php-7.3.4.tar.bz2
RUN tar -xvf php-7.3.4.tar.bz2 -C /source/php
#COPY php-7.3.4 /source/php/php-7.3.4
WORKDIR /source/php/php-7.3.4
RUN mkdir -p /usr/local/curl/7.48.0/include
RUN ln -s /usr/include/x86_64-linux-gnu/curl /usr/local/curl/7.48.0/include/curl
RUN ./configure --prefix=/usr/local/php/7.3.4 --enable-fpm --with-config-file-path=/usr/local/etc/php --with-gettext=/usr/local/gettext/0.19 --with-mcrypt=/usr/local/libmcrypt/2.5.8 --with-zlib-dir=/usr/local/zlib/1.2.8 --with-curl=/usr/local/curl/7.48.0/ --with-mhash=/usr/local/mhash/0.9.9.9 --with-jpeg-dir=/usr/local/libjpeg/9b --with-png-dir=/usr/local/libpng/1.6.21 --with-freetype-dir=/usr/local/freetype/2.6.3 --with-iconv=/usr/local/libiconv/1.14 --enable-mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --enable-wddx --enable-ftp --enable-sockets --enable-mbstring --enable-bcmath --enable-soap --enable-json --with-readline --with-libedit --with-openssl --enable-pcntl --enable-exif 
RUN make && make install
#####################php end
##################### autoconf unzip cmake
RUN apt-get install -y m4  autoconf unzip cmake
WORKDIR /source/
RUN wget http://pecl.php.net/get/amqp-1.9.4.tgz
RUN wget https://github.com/alanxz/rabbitmq-c/archive/master.zip
RUN mkdir /source/amqp
RUN tar -xvf amqp-1.9.4.tgz -C /source/amqp
RUN unzip master.zip -d /source/
RUN mkdir /source/rabbitmq-c-master/build
WORKDIR /source/rabbitmq-c-master/build
RUN cmake  -DCMAKE_INSTALL_PREFIX=/usr/local/rabbitmq-c ..
RUN make && make install
RUN ln -s /usr/local/rabbitmq-c/lib/x86_64-linux-gnu/librabbitmq.so  /usr/lib/librabbitmq.so && ln -s /usr/local/rabbitmq-c/lib/x86_64-linux-gnu/librabbitmq.so.4  /usr/lib/librabbitmq.so.4
WORKDIR /source/amqp/amqp-1.9.4/
RUN /usr/local/php/7.3.4/bin/phpize 
RUN ./configure  --with-php-config=/usr/local/php/7.3.4/bin/php-config --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq-c
RUN make && make install
RUN groupadd nobody
WORKDIR /source
RUN wget https://xdebug.org/files/xdebug-2.7.0.tgz
RUN tar -xvf xdebug-2.7.0.tgz
WORKDIR /source/xdebug-2.7.0
RUN /usr/local/php/7.3.4/bin/phpize
RUN ./configure --with-php-config=/usr/local/php/7.3.4/bin/php-config
RUN make && make install

RUN apt-get install libzip4 libzip-dev
WORKDIR /source/php/php-7.3.4/ext/zip
RUN /usr/local/php/7.3.4/bin/phpize
RUN ./configure --with-php-config=/usr/local/php/7.3.4/bin/php-config
RUN make && make install

WORKDIR /source/php/php-7.3.4/ext/gd
RUN apt-get install libpng-dev

#RUN apt-get -y install python graphviz
#RUN apt-get -y install python-pip
#RUN pip install gprof2dot




WORKDIR /source/
RUN wget http://pecl.php.net/get/imagick-3.4.3RC4.tgz
RUN tar -xvf imagick-3.4.3RC4.tgz
WORKDIR /source/imagick-3.4.3RC4/
RUN /usr/local/php/7.3.4/bin/phpize 
RUN ./configure  --with-php-config=/usr/local/php/7.3.4/bin/php-config
RUN make && make install


EXPOSE 9000
EXPOSE 9001
CMD ["/usr/local/php/7.3.4/sbin/php-fpm","-F"]

