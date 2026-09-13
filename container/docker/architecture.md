# Docker Architecture

Docker follows a client-server architecture, where all the docker clients talk to docker daemon, which does all the heavy lifting of building running and distributing docker containers. The Docker client and daemon can run on the same system, or can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface. Another Docker client is Docker Compose, that works with applications consisting of a set of containers.

![Docker Architecture](/asset/images/docker/docker_architecture.png)

Docker daemon runs as a process in the host OS, and uses the host OS hence making the clients running very light weight.

* The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

* The Docker client (docker) is the primary way that many Docker users interact with Docker. While using the commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon

---

## Links

* <https://docs.docker.com/get-started/overview/>
* <https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction#background

