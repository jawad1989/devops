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

## Configure users for Gui and admin

```
docker exec -it <container-id> bash
cd /usr/local/tomcat/conf
vi tomcat-users.xml
```
enter below lines at the end 
```
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="admin" password="password" roles="manager-gui,manager-script" />
<user username="tomcat" password="tomcat" roles="manager-gui"/>

```
exit and stop/start the docker container

```
docker stop <container-id>
docker start <container-id>
```
goto tomcat in browser press __MANAGER APP__ button on right side, enter credentials which you set earlier.

![tomcatServer](https://github.com/jawad1989/devops/blob/master/projects/sonarqube-jenkins/2%20-%20tom%20cat%20server.PNG)
