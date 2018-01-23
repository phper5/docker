# shadowsocks客户端
启动脚本参考 

参考脚本
`docker build -t coder5/shadowsocks .`

`docker run -d -p 1080:1080 --name=socks  -v /data/etc/shadowsocks/:/etc/shadowsocks coder5/shadowsocks`
默认使用的配置 /etc/shadowsocks/007.js
提供的端口 1080
