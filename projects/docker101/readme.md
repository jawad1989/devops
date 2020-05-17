# Introduction to Docker 

## What is a Container
* [What is Container](https://www.docker.com/resources/what-container)

## Pre Reqs
* [Installing Docker Enginer](https://docs.docker.com/engine/install/) See the official docker website for installing docker
* If you are running docker from a non root user, you shpuld add your user to `docker` group with below command:
```
sudo usermod -aG docker your-user
```

## Check Your Enviornment
*  List Version of Docker ```docker --version```
Docker version 19.03.5, build 633a0ea

## Running Hello World Container

1. Testing that our installation was successful by running Docker Hello-World Image from docker hub.

```sh
docker run hello-world

    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    ca4f61b1923c: Pull complete
    Digest: sha256:ca0eeb6fb05351dfc8759c20733c91def84cb8007aa89a5bf606bc8b315b9fc7
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    ...
```

2. Run `docker image ls` to list the hello-world image that we downloaded on our machine.
3. List hello-world container by running below command. add `--all` if container is stopped.
```
docker ps
  CONTAINER ID     IMAGE           COMMAND      CREATED            STATUS
  54f4984ed6a8     hello-world     "/hello"     20 seconds ago     Exited (0) 19 seconds ago
```

## Docker Hub and running Pre built images

The best feature of docker is you can download and use 1000's of pre built images available to you with a single command e.g. wordrpress, ubuntu, jenkins, node.js etc.
we will use some of the images and run them to get you started:

### 1. Running HTTPD Server

```
docker run --name apache -p 8080:80 httpd:2.4

or 

docker run -d --name apache2 -p 8082:80 httpd:2.4
```

To get more info about a container
```
docker logs apache2
docker stats apache2
```

**go in your container and start playing with it**

In the container, we'll be root right off and be sitting in the `/usr/local/apache2 directory`. Run a quick `ls` to see what's here, and then cd htdocs to get into where the website's index.html page is.

```
docker exec -it apache2 bash
cd htdocs/
touch jawad.html
echo 'hello jawad how are you?' > jawad.html
exit
```

now if you will goto `localhost:8082/jawad.html` you will see the new file.


## 2. Running a static HTML website in docker

lets say we have a directory `mySite` and it has two files one `HTML` other `CSS` and we want to run them on a webserver i.e. `nginx`:

```
jawad@DockerLab:~/images/mySite$ ls
  index.html  mystyle.css
jawad@DockerLab:~/images/mySite$ pwd
/home/jawad/images/mySite
```

Create your docker file for building your image, first line defines the base image and second one copies our content of current directory to a particular directory

```
gedit Dockerfile

FROM nginx:alpine
COPY . /usr/share/nginx/html
```

build the image and name it `webserver-image:v1`

```
docker build -t webserver-image:v1 .
docker images
```

run the docker container using our image 
```
docker run -d -p 8084:80 webserver-image:v1
```

you will see your static website up and running at `http://locahost:8084`

## 2. Running Wordpress image

You can read about wordpress image at [Docker Hub - Wordress](https://hub.docker.com/_/wordpress)


