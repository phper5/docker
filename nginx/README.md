```
docker build -t coder5/nginx .
```
```
docker run -d  --hostname=nginx --name nginx -p 80 --net=app  -v /data/code/html:/data/html -v  /data/etc/nginx/conf:/usr/local/nginx/conf/  -v /data/log/nginx:/data/log/nginx coder5/nginx /usr/local/nginx/sbin/nginx
```






