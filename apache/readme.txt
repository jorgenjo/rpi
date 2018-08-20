TEST

docker build -t "apache" .

docker run -d --restart=always -p 8084:80 -t apache:latest

