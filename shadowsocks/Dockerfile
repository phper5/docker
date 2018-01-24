FROM ubuntu:14.04
ENV UPDATE_AT 20180122
RUN apt-get update
RUN apt-get install -y  python-gevent python-pip
RUN pip install shadowsocks
ADD shadowsocks /usr/bin/shadowsocks
RUN chmod +x /usr/bin/shadowsocks
EXPOSE 1080
EXPOSE 8388
ENTRYPOINT ["/usr/bin/shadowsocks"]
CMD ["server"]

