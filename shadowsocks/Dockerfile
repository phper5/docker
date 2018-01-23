FROM ubuntu:14.04
ENV UPDATE_AT 20171205
RUN apt-get update
RUN apt-get install -y  python-gevent python-pip
RUN pip install shadowsocks
EXPOSE 1080
CMD ["sslocal","-c","/etc/shadowsocks/007.js"]

