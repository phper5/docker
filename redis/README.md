docker build -t coder5/redis .

docker run --name redis -v /data/etc/redis/:/etc/redis/ -v /data/data/redis:/data/data/redis -v /data/log/redis:/data/log/redis  --hostname redis -d coder5/redis
