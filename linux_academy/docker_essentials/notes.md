Docker Quick Start
==================

Installation and Configuration
------------------------------

For RPM systems add the following to `/etc/yum.repos.d/docker.repo`:

```
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/(distro)/(version)/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
```

This will allow you to install the latest docker.

Once installed enable and start the docker service with `systemctl`.

To enable a user to run docker run `usermod -a -G docker $user` (does not work on atomic systems).


The Docker Hub
--------------

The docker hub is located at https://hub.docker.com and with an account lets you host unlimited public containers and 1 private container by default.

Containers are build in layers. The base image is what the container is built on. The base is immutable and changes are layerd on top until you have a completed image. Running containers have file changes on the top layer that is lost with the container.


Base Images
------------

Containers need a base with files and libraries that the serivce needs to run as well as a kernel. Container bases are typically built off a Linux disto. 

To pull base images decide what to use for a base and run `docker pull $image`. To specify a version of an image you can specify a tag like `image:tag`. This can be done with the RUN key in a Dockerfile.

To find images use `docker search $term`

You can view the configuration of a container image with `docker inspect`.


Running Containers
------------------

You can view running containers with `docker ps` which will give you stats and how long it has been run. Some containers quit when the command completes so it will not appear there without a `-a` flag which would show all containers run.

To stay attached to the container when running you can use the `-it` flags which are for interactive and connect to terminal. 

To keep the container running you can use `-d` with some program running to keep it up. `-d` does not work without a program being run.

When running a serivce on a container it is attached to the defualt docker network on the machine and can be accesd by the containers IP address.

When running a container you can specify a name with `--name=` and names are unique so it can not be reused while that container exists.


The Container Lifecycle
------------------------

The first time you run a container it is done with `docker run`. The container stops when the program completes or when you run `docker stop`.

When a container has stopped you can restart it with `docker start $containerName`.

You can attach a running container with `docker attach` (warning this attaches to the process, usually not going to be a shell). To attach with a shell run `docker exec -it $containerName /bin/bash`. 


Images and Container Management
---------------------------------

Clean your docker enviroment with `docker system prune` or you can specify what with replacing system with container, image, network, volume.

To remove old images run `docker rmi $image`. This will fail if a container is dependant on the image but can be overide with a `-f` flag.

Cleaning containers is the same but with `docker rm`.

To remove all containers you can run `docker rm $(docker container ls -a -q)`
