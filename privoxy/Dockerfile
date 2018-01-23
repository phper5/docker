FROM ubuntu:14.04
ENV UPDATE_AT 20171205
RUN apt-get update
RUN apt-get install -y  privoxy
EXPOSE 1070
CMD ["privoxy","--no-daemon","/etc/privoxy/config"]

