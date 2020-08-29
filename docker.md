# docker

This is my cheatsheet for anything related to `docker`

* How to list the running containers?

```bash
$ docker ps
```

* How to list all the running containers including the stopped ones?

```bash
$ docker ps -a
```

* How to start a stopped container?

```bash
$ docker start <container-id-or-name>
```

* How to stop a running container?

```bash
$ docker stop <container-id-or-name>
```

* How to remove a stopped container?

```bash
$ docker rm <container-id-or-name>
```

* How to remove a running container?

```bash
$ docker rm --force <container-id-or-name>
$ # or
$ docker rm -f <container-id-or-name>
```

* How to know all the images present in my machine?

```bash
$ docker images
```

* How to build images?

```bash
$ # uses Dockerfile in the directory where the command is being run
$ docker build -t <image-tag> <dir>
$ # to use a specific Dockerfile
$ docker build -t <image-tag> -f <Dockerfile-path> <dir> 
```

* How to pull images from a docker registry?

```bash
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

```bash
$ # for pushing to docker hub
$ docker push <image-name-path>
$ # an example
$ docker push karuppiah7890/utils
$ # more generic push
$ docker push <registry-host-with-port-if-any>/<image-name-path>:<image-tag>
$ # another example
$ docker push my-private-artifactory.io:6555/karuppiah7890/utils:1.2
```

* How to delete images in my machine?

```bash
$ docker image rm <image-id-or-image-name-with-tag>
$ # examples
$ docker image rm redis:5.0.7
$ # removing the latest tag of ubuntu
$ docker image rm ubuntu
$ # image id
$ docker image rm 4e5021d210f6 
```

* How to check the resource usage (CPU, Memory) of my containers?

```bash
$ docker stats
```

* How to search Docker Hub for images?

I usually search in the web browser at the link - https://hub.docker.com/search/?q=search%20query&type=image

```bash
$ docker search <search-string>
$ # example
$ docker search postgres
```

* How to tag already built images?

```bash
$ docker tag source_image[:tag] target_image[:tag]
$ # example
$ docker tag existingImage:existingTag newImageName:newImageTag
```

* How to login to Docker Hub or any docker registry?

```bash
$ # For docker hub
$ docker login
$ # For other docker image registries
$ docker login <image-registry-url>
```

* How to logout from Docker Hub or any docker registry?

```bash
$ # For docker hub
$ docker logout
$ # For other docker image registries
$ docker logout <image-registry-url>
```

* How to check the logs of a docker container?

```bash
$ docker logs <container-id-or-name>
$ # to continuously stream / follow the logs use -f
$ docker logs -f <container-id-or-name>
```

* How to copy files from my local machine to container and vice versa?

```bash
$ # it's similar to cp command in *nix systems.
$ # it's best to use absolute paths to avoid any confusions or issues.
$ # from container to local machine.
$ docker cp <container-id-or-name>:<src-path-inside-container> <dest-path-in-local>
$ # from local machine to container.
$ docker cp <src-path-in-local> <container-id-or-name>:<dest-path-inside-container>
```

* How to execute a command inside a container?

```bash
$ # it will not work out if the command does not exist in the container.
$ # the command has to be present / installed in the container and present in
$ # the $PATH environment variable.
$ docker exec <container-id-or-name> <command-name>
$ # for an interactive console - for running a shell inside the container etc
$ docker exec --interactive --tty <container-id-or-name> <command-name>
$ # example with short flags
$ docker exec -i -t ubuntu bash
$ docker exec -it ubuntu bash
```

* How to get inside the container's shell? To check files, run commands
and more, in an interactive manner

If the container has `sh` or `bash` installed, then do this

```bash
$ docker exec --interactive --tty <container-id-or-name> sh
$ docker exec --interactive --tty <container-id-or-name> bash
$ # shorter version is
$ docker exec -it <container-id-or-name> sh
$ docker exec -it <container-id-or-name> bash
```
