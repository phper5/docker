FROM ubuntu:14.04
ENV UPDATE_AT 20171205
RUN apt-get update
RUN sudo apt-get install -y build-essential
RUN sudo apt-get install -y libpcre3 libpcre3-dev zlib1g-dev libssl-dev  wget
RUN mkdir -p /source/nginx
WORKDIR /source
RUN wget http://nginx.org/download/nginx-1.12.2.tar.gz -O nginx.tar.gz
RUN tar -xvf nginx.tar.gz -C /source/nginx
WORKDIR /source/nginx/nginx-1.12.2
RUN ./configure
RUN make && make install
EXPOSE 80

