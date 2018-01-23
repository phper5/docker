docker build -t coder5/redis .

docker run --name redis  --hostname redis -d coder5/redis
