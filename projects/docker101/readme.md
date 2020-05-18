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

## 3. Creating Tomcat server in Docker Container

[Tomcat server as service](https://github.com/jawad1989/devops/tree/master/projects/tomcat-docker)

## 4. Data Containers

Data containers are containers whose sole responsibility is to be a place to store/manage data.
Like other containers they are managed by the host system. However, they don't run when you perform a docker ps command.

To create a Data Container we first create a container with a well-known name for future reference. We use busybox as the base as it's small and lightweight in case we want to explore and move the container to another host.

When creating the container, we also provide a -v option to define where other containers will be reading/saving data.

```
docker create -v /config --name dataContainer busybox
docker cp config.conf dataContainer:/config/
docker run --volumes-from dataContainer ubuntu ls /config
```

## 5. Docker Volumes

Docker volumes are used to persist data from within a Docker container. There are a few different types of Docker volumes: host, anonymous, and, named. Knowing what the difference is and when to use each type can be difficult, but hopefully, I can ease that pain here.

* Host Volumes
A host volume can be accessed from within a Docker container and is stored on the host, as per the name. To create a host volume, run:
```
docker run -v /path/on/host:/path/in/container
```

* Anonymous Volumes
The location of anonymous volumes is managed by Docker. Note that it can be difficult to refer to the same volume when it is anonymous. To create an anonymous volume, run:
```
docker run -v /path/in/cntainer ...
```

* Named Volumes
Named volumes and anonymous volumes are similar in that Docker manages where they are located. However, as you might guess, named volumes can be referred to by specific names. To create a named volume, run:
```
docker volume create somevolume
docker run -v name:/path/in/container
```

### Example:  Create a volume on host and place a static website, bind that volume with nginx and run the contianer using below command

Static Website at host: /images/mySite
Volume at VM: /usr/share/nginx/html
container Name: siteUsingVol
Image Name: nginx

```
docker run --name:siteUsingVol -d -v /images/mySite:/usr/share/nginx/html -p 5000:80 nginx
```

Now put any index.html in `/images/mySite` at host and you can see the file in VM `localhost:5000/`

### Copying files between containers from a shared volume

Creating volume
```
docker volume create devops_volume
docker volume ls
```

Creating container with the volume attached to them
docker container create --name <container_name> -it --mount source<volume_name>,target=/<folder_Name> <image_name>

```
docker container create --name myBusyBox1 -it --mount source=devops_volume,target=/app busybox
docker container create --name myBusyBox2 -it --mount source=devops_volume,target=/app busybox
```

copying files between containers from a shared volume
```
docker exec -it myBusyBox1 sh
cd /app
mkdir devops
exit
```
copy a file frm host to myBusyBox1
```
docker container cp index.html myBusyBox1:/app/devops/
```

connect to 2nd container to see the file if created, you can sh the container and see the file and folder there




## 6. Communicating between containers using links
This scenario explores how to allow multiple containers to communicate with each other. The steps will explain how to connect a data-store, in this case, Redis, to an application running in a separate container.

```
docker run -d --name redis-server redis
```
In this example, we bring up a Alpine container which is linked to our redis-server. We've defined the alias as redis. When a link is created, Docker will do two things.

First, Docker will set some environment variables based on the linked to the container. These environment variables give you a way to reference information such as Ports and IP addresses via known names.

You can output all the environment variables with the env command. For example:

```
docker run --link redis-server:redis alpine env
```
Secondly, Docker will update the HOSTS file of the container with an entry for our source container with three names, the original, the alias and the hash-id. You can output the containers host entry using cat /etc/hosts
```
docker run --link redis-server:redis alpine cat /etc/hosts
```
we can ping the source container
```
docker run --link redis-server:redis alpine ping -c 1 redis
```

Example app
```
docker run -d -p 3000:3000 --link redis-server:redis katacode/redis-note-docker-example
curl docker:3000
```

Connet to redis cli
```
docker run -it --link redis-server:redis redis redis-cli -h redis
KEYS *
QUIT
```

## 6. Share your images on Docker Hub

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



## 7. Useful Commands

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

Remove all containers
```
docker rm –f $(docker ps -aq)
```

remove volume
```
docker volume rm <volume_name>
```

remove all volumes at once
```
docker volume prune
```
