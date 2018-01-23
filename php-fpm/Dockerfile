FROM coder5/gcc
RUN apt-get update --fix-missing
RUN apt-get install -y wget
RUN mkdir -p /source/php
WORKDIR /source
RUN wget http://cl1.php.net/distributions/php-7.1.11.tar.gz
RUN tar -xvf php-7.1.11.tar.gz -C /source/php
WORKDIR /source/php/php-7.1.11
#RUN apt-get install -y build-essential
#准备环境
#libxml2
RUN apt-get install -y libxml2-dev
#OpenSSL
RUN  apt-get install -y openssl 
RUN  apt-get install -y libssl-dev
RUN mkdir -p /usr/local/openssl/include/openssl/
RUN ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h
RUN mkdir -p /usr/local/openssl/lib/
RUN ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a
RUN ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/
#curl
RUN apt-get install  -y curl 
RUN apt-get install -y libcurl3 libcurl3-dev
# iconv library
WORKDIR /source/
RUN wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz
RUN tar -xvf libiconv-1.15.tar.gz
WORKDIR /source/libiconv-1.15
RUN ./configure
RUN make && make install

#libmcrypt
RUN apt-get install -y libmcrypt-dev
#libedit
RUN apt-get install  -y libedit-dev
WORKDIR /source/php/php-7.1.11
RUN ./configure --prefix=/usr/local/php/7.1.11 --enable-fpm --with-config-file-path=/usr/local/etc/php --with-gettext=/usr/local/gettext/0.19 --with-mcrypt=/usr/local/libmcrypt/2.5.8 --with-zlib-dir=/usr/local/zlib/1.2.8 --with-curl=/usr/local/curl/7.48.0/ --with-mhash=/usr/local/mhash/0.9.9.9 --with-jpeg-dir=/usr/local/libjpeg/9b --with-png-dir=/usr/local/libpng/1.6.21 --with-freetype-dir=/usr/local/freetype/2.6.3 --with-iconv=/usr/local/libiconv/1.14 --enable-mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --enable-wddx --enable-ftp --enable-sockets --enable-mbstring --enable-bcmath --enable-soap --enable-json --with-readline --with-libedit --with-openssl --enable-pcntl --enable-exif 
RUN make && make install

##相关扩展
RUN apt-get install -y m4  autoconf unzip cmake
WORKDIR /source/
RUN wget http://pecl.php.net/get/amqp-1.9.3.tgz
RUN wget https://github.com/alanxz/rabbitmq-c/archive/master.zip
RUN mkdir /source/amqp
RUN tar -xvf amqp-1.9.3.tgz -C /source/amqp
RUN unzip master.zip -d /source/
RUN mkdir /source/rabbitmq-c-master/build
WORKDIR /source/rabbitmq-c-master/build
RUN cmake ..
RUN make && make install
WORKDIR /source/amqp/amqp-1.9.3/
RUN /usr/local/php/7.1.11/bin/phpize 
RUN ./configure  --with-php-config=/usr/local/php/7.1.11/bin/php-config
RUN make && make install
RUN apt-get install -y zlib1g-dev && /usr/local/php/7.1.11/bin/pecl install grpc-1.7.0  && /usr/local/php/7.1.11/bin/pecl install protobuf-3.4.0
RUN apt-get install -y zip
###php-fpm
RUN groupadd nobody
WORKDIR /source
RUN wget https://xdebug.org/files/xdebug-2.5.5.tgz
RUN tar -xvf xdebug-2.5.5.tgz
WORKDIR xdebug-2.5.5
RUN /usr/local/php/7.1.11/bin/phpize
RUN ./configure --with-php-config=/usr/local/php/7.1.11/bin/php-config
RUN make && make install
RUN apt-get -y install graphviz  python
WORKDIR /source
RUN wget http://pecl.php.net/get/swoole-1.10.0.tgz
RUN tar -xvf swoole-1.10.0.tgz
WORKDIR /source/swoole-1.10.0
RUN /usr/local/php/7.1.11/bin/phpize
RUN ./configure --with-php-config=/usr/local/php/7.1.11/bin/php-config
RUN make && make install
EXPOSE 9000
CMD ["/usr/local/php/7.1.11/sbin/php-fpm","-F"]




