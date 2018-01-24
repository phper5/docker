# shadowsocks客户端
启动脚本参考 

参考脚本
```
docker build -t coder5/shadowsocks .
`````

```
作为客户端启动
docker run -d -p 1080:1080 --name=socks  -v /data/etc/shadowsocks/:/etc/shadowsocks coder5/shadowsocks  client
或者
docker run -d -p 1080:1080 --name=socks  -v /data/etc/shadowsocks/:/etc/shadowsocks coder5/shadowsocks  client pathToConfig

作为服务端启动
docker run -d -p 8388:8388 --name=socks  -v /data/etc/shadowsocks/:/etc/shadowsocks
或者
docker run -d -p 8388:8388 --name=socks  -v /data/etc/shadowsocks/:/etc/shadowsocks coder5/shadowsocks  server
或者
docker run -d -p 8388:8388 --name=socks  -v /data/etc/shadowsocks/:/etc/shadowsocks coder5/shadowsocks  server pathToConfig

```
默认使用的配置     
/etc/shadowsocks/007.js    
/etc/shadowsocks/server.js

提供的端口    
1080    
8388
