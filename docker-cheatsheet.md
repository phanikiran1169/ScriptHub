## Containers
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings.
For more information on containers and how they are different from virtual machines, check this [link](https://www.docker.com/resources/what-container/)

### Lifecycle

* [`docker create`](https://docs.docker.com/engine/reference/commandline/create) creates a container but does not start it.
* [`docker rename`](https://docs.docker.com/engine/reference/commandline/rename/) allows the container to be renamed.
* [`docker run`](https://docs.docker.com/engine/reference/commandline/run) creates and starts a container in one operation.
* [`docker rm`](https://docs.docker.com/engine/reference/commandline/rm) deletes a container.
* [`docker update`](https://docs.docker.com/engine/reference/commandline/update/) updates a container's resource limits.

Normally if you run a container without options it will start and stop immediately, but if you want to keep it running you can use the command, `docker run -td container_id` this will use the option `-t` that will allocate a pseudo-TTY session and `-d` that will detach automatically the container (run container in background and print container ID).

If you want more information on the `docker run -it image_id`, refer [here](https://stackoverflow.com/questions/48368411/what-is-docker-run-it-flag).

If you want a transient container, `docker run --rm` will remove the container after it stops.

If you want to map a directory on the host to a docker container, `docker run -v $HOSTDIR:$DOCKERDIR`. Also, see [Volumes]().

If you want to remove also the volumes associated with the container, the deletion of the container must include the `-v` switch like in `docker rm -v`.

There's also a [logging driver](https://docs.docker.com/engine/admin/logging/overview/) available for individual containers in docker. To run docker with a custom log driver (i.e., to syslog), use `docker run --log-driver=syslog`.

Another useful option is `docker run --name yourname docker_image` because when you specify the `--name` inside the run command this will allow you to start and stop a container by calling it with the name the you specified when you created it.

### Starting and Stopping

* [`docker start`](https://docs.docker.com/engine/reference/commandline/start) starts a container so it is running.
* [`docker stop`](https://docs.docker.com/engine/reference/commandline/stop) stops a running container.
* [`docker restart`](https://docs.docker.com/engine/reference/commandline/restart) stops and starts a container.
* [`docker pause`](https://docs.docker.com/engine/reference/commandline/pause/) pauses a running container, "freezing" it in place.
* [`docker unpause`](https://docs.docker.com/engine/reference/commandline/unpause/) will unpause a running container.
* [`docker wait`](https://docs.docker.com/engine/reference/commandline/wait) blocks until running container stops.
* [`docker kill`](https://docs.docker.com/engine/reference/commandline/kill) sends a SIGKILL to a running container.
* [`docker attach`](https://docs.docker.com/engine/reference/commandline/attach) will connect to a running container.

If you want to detach from a running container, use `Ctrl + p, Ctrl + q`.
If you want to integrate a container with a [host process manager](https://docs.docker.com/engine/admin/host_integration/), start the daemon with `-r=false` then use `docker start -a`.

If you want to expose container ports through the host, see the [exposing ports](#exposing-ports) section.

Restart policies on crashed docker instances are [covered here](https://docs.docker.com/config/containers/start-containers-automatically/).

### exposing-ports
By default, when you run a container, none of the container's ports are exposed to the host. This means you won't be able to access any ports that the container might be listening on. To make a container's ports accessible from the host, you need to publish the ports.

You can start the container with the `-P` or `-p` flags to expose its ports:

- The `-P` (or `--publish-all`) flag publishes all the exposed ports to the host. Docker binds each exposed port to a random port on the host.
- The `-P` flag only publishes port numbers that are explicitly flagged as exposed, either using the Dockerfile `EXPOSE` instruction or the `--expose` flag for the docker run command.
- The `-p` (or `--publish`) flag lets you explicitly map a single port or range of ports in the container to the host.

The port number inside the container (where the service listens) doesn't need to match the port number published on the outside of the container (where clients connect). For example, inside the container, an HTTP service might be listening on port 80. At runtime, the port might be bound to 42800 on the host. To find the mapping between the host ports and the exposed ports, use the docker port command.

`docker run -p $HOSTPORT:$CONTAINERPORT --name containername imagename`


## Dockerfile

[The configuration file](https://docs.docker.com/engine/reference/builder/). Sets up a Docker container when you run `docker build` on it. Vastly preferable to `docker commit`.  

### Instructions

* [.dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file)
* [FROM](https://docs.docker.com/engine/reference/builder/#from) Sets the Base Image for subsequent instructions.
* [MAINTAINER (deprecated - use LABEL instead)](https://docs.docker.com/engine/reference/builder/#maintainer-deprecated) Set the Author field of the generated images.
* [RUN](https://docs.docker.com/engine/reference/builder/#run) execute any commands in a new layer on top of the current image and commit the results.
* [CMD](https://docs.docker.com/engine/reference/builder/#cmd) provide defaults for an executing container.
* [EXPOSE](https://docs.docker.com/engine/reference/builder/#expose) informs Docker that the container listens on the specified network ports at runtime.  NOTE: does not actually make ports accessible.
* [ENV](https://docs.docker.com/engine/reference/builder/#env) sets environment variable.
* [ADD](https://docs.docker.com/engine/reference/builder/#add) copies new files, directories or remote file to container.  Invalidates caches. Avoid `ADD` and use `COPY` instead.
* [COPY](https://docs.docker.com/engine/reference/builder/#copy) copies new files or directories to container.  By default this copies as root regardless of the USER/WORKDIR settings.  Use `--chown=<user>:<group>` to give ownership to another user/group.  (Same for `ADD`.)
* [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) configures a container that will run as an executable.
* [VOLUME](https://docs.docker.com/engine/reference/builder/#volume) creates a mount point for externally mounted volumes or other containers.
* [USER](https://docs.docker.com/engine/reference/builder/#user) sets the user name for following RUN / CMD / ENTRYPOINT commands.
* [WORKDIR](https://docs.docker.com/engine/reference/builder/#workdir) sets the working directory.
* [ARG](https://docs.docker.com/engine/reference/builder/#arg) defines a build-time variable.
* [ONBUILD](https://docs.docker.com/engine/reference/builder/#onbuild) adds a trigger instruction when the image is used as the base for another build.
* [STOPSIGNAL](https://docs.docker.com/engine/reference/builder/#stopsignal) sets the system call signal that will be sent to the container to exit.
* [LABEL](https://docs.docker.com/config/labels-custom-metadata/) apply key/value metadata to your images, containers, or daemons.
* [SHELL](https://docs.docker.com/engine/reference/builder/#shell) override default shell is used by docker to run commands.
* [HEALTHCHECK](https://docs.docker.com/engine/reference/builder/#healthcheck) tells docker how to test a container to check that it is still working.

### Examples

* [Examples](https://docs.docker.com/engine/reference/builder/#dockerfile-examples)
* [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)

## Layers

The versioned filesystem in Docker is based on layers. They're like [git commits or changesets for filesystems](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/).
