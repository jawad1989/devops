# Installing Docker
```
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker ec2-user
```
# Test Docker
```
docker run hello-world
```
# Installing Tomcat
```
git clone https://github.com/jawad1989/docker-tomcat.git
ls
```

# Search image
```
docker search tomcat
```

# Dockerfile
```
FROM tomcat:8.0-alpine
LABEL maintainer="jawadsalim12@gmail.com"

ADD sample.war /usr/local/tomcat/webapps/

EXPOSE 8080
CMD ["catalina.sh", "run"]
```

# Build Docker File
```
docker build -t mywebapp .

docker image ls
docker run -p 80:8080 mywebapp
```

# Try Tomcat in Browser and your app
```
http://localhost:80/ 
http://localhost:80/sample
```
