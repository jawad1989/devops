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


## 2. Running a static website in docker

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

## 2. Deploying Node.js Application

For complete details and steps goto [Docker Docks - Building a Node js App](https://docs.docker.com/get-started/part2/)

we will only see the Dockerfile

```
# Use the official image as a parent image.
FROM node:current-slim

# Set the working directory.
WORKDIR /usr/src/app

# Copy the file from your host to your current location.
COPY package.json .

# Run the command inside your image filesystem.
RUN npm install

# Inform Docker that the container is listening on the specified port at runtime.
EXPOSE 8080

# Run the specified command within the container.
CMD [ "npm", "start" ]

# Copy the rest of your app's source code from your host to your image filesystem.
COPY . .
```


You can read about wordpress image at [Docker Hub - Wordress](https://hub.docker.com/_/wordpress)


### Share your images on Docker Hub

This step helps you in developing a containerized application is to share your images on a registry like Docker Hub, so they can be easily downloaded and run on any destination machine

1. Visit the Docker Hub sign up page, https://hub.docker.com/signup.

2. Fill out the form and submit to create your Docker ID.

3. Verify your email address to complete the registration process.

4. Click on the Docker icon in your toolbar or system tray, and click Sign in / Create Docker ID.

5. Fill in your new Docker ID and password. After you have successfully authenticated, your Docker ID appears in the Docker Desktop menu in place of the ‘Sign in’ option you just used.

Lets say you have an image named `mywebserver` and you want to deploy it on docker hub. images must be namespaced correctly to share on Docker Hub. Specifically, you must name images like `<Docker ID>/<Repository Name>:<tag>`. You can relabel your `NodejsServer:1.0` image like this (of course, please replace `jawadxiv` with your Docker ID):

`docker tag mywebserver:1.0 jawadxiv/NodejsServer:1.0`

Finally you push image to docker hub:

`docker push jawadxiv/NodejsServer:1.0`

You can pull using below command in any of your enviornment:

`docker pull jawadxiv/NodejsServer:1.0`
`docker pull jawadxiv/NodejsServer:1.0`



## Useful Commands

interactive shell contianer using image
```
docker run -it image_name sh
```

following the images with `entrypoint'
```
docker run -it --entrypoint sh image_name
```

if you want to see how the image was build, meaning the steps in its Dockerfile, you can:

```
docker image history --no-trunc image_name > image_history
```
