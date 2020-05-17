# Introdcution to Docker 

## What is a Container
* [What is Container](https://www.docker.com/resources/what-container)

## Pre Reqs
* [Installing Docker Enginer](https://docs.docker.com/engine/install/) See the official docker website for installing docker

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

### 1. Running wordpress image

