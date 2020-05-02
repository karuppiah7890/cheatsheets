# docker

This is my cheatsheet for anything related to `docker`

* How to list the running containers?

```
$ docker ps
```

* How to list all the running containers including the stopped ones?

```
$ docker ps -a
```

* How to start a stopped container?

```
$ docker start <container-id-or-name>
```

* How to stop a running container?

```
$ docker stop <container-id-or-name>
```

* How to remove a stopped container?

```
$ docker rm <container-id-or-name>
```

* How to remove a running container?

```
$ docker rm --force <container-id-or-name>
$ # or
$ docker rm -f <container-id-or-name>
```

* How to know all the images present in my machine?

```
$ docker images
```

* How to build images?

```
$ # uses Dockerfile in the directory where the command is being run
$ docker build -t <image-tag> <dir>
$ # to use a specific Dockerfile
$ docker build -t <image-tag> -f <Dockerfile-path> <dir> 
```

* How to pull images from a docker registry?

```
$ # for pulling from docker hub
$ docker pull <image-name>
$ # examples for docker hub
$ docker pull ubuntu
$ docker pull karuppiah7890/utils
$ # more generic docker pull
$ docker pull <registry-host-with-port-if-any>/<image-name-path>:<image-tag>
$ # another example
$ docker pull my-private-artifactory.io:6555/karuppiah7890/utils:1.2
```

* How to push images to a docker registry?

* How to delete images in my machine?

* How to check the resource usage (CPU, Memory) of my containers?

```
$ docker stats
```

* How to search Docker Hub for images?

* How to tag already built images?

* How to login to Docker Hub or any docker registry?

* How to logout from Docker Hub or any docker registry?

* How to check the logs of a docker container?

* How to copy files from my local machine to container and vice versa?


