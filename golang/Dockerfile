FROM ubuntu:14.04
ENV UPDATE_AT 20171205
RUN apt-get update
RUN sudo apt-get install -y wget
RUN wget https://dl.google.com/go/go1.9.3.linux-amd64.tar.gz
RUN tar -C /usr/local/ -xzf go1.9.3.linux-amd64.tar.gz
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/will && \
    echo "will:x:${uid}:${gid}:will,,,:/home/will:/bin/bash" >> /etc/passwd && \
    echo "will:x:${uid}:" >> /etc/group && \
    echo "will ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/will && \
    chmod 0440 /etc/sudoers.d/will && \
    chown ${uid}:${gid} -R /home/will
USER will
WORKDIR /home/will/go
ENTRYPOINT ["go"]
CMD ["help"]
