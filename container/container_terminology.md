# What are containers?

A container is really two different things, Like a Linux program it has two different states:

* rest : when at rest a container is a file (or set of files) that is saved on the disk. This is referred to as
  container image or container repository.
* running: While running a container it's nothing but a linux process.

While running the container start command the container engine unpacks the required files and metadata, then hands them
off to Linux kernel. Starting a container is very similar to starting a normal Linux process and requires making an API
call to the Linux kernel. This API call typically initiates extra isolation and mounts a copy of the files that were in
the container image.

## Vocabulary

Common terms used in container world:

### Container Image

> A file pulled from container repository and used as mount point when starting the container.

### Container Image Format

> A specialized file format, that the container engine understands. Traditionally all the container engine provider
> used to have there specific format, though now everyone uses Open Container Initiative (OCI). Essentially, the OCI
> format defines a container image composed of tar files for each layer, and a manifest.json file with the metadata.

### Container Engine

> A container engine is a piece of software that accepts user requests, including command line options, pulls images and
> from the end user's perspective runs the container. Most container engines don't actually run the containers, they
> rely on an OCI compliant runtime like **_runc_**.
>
> Typically, the container engine is responsible:
> * Handling user input
> * Handling input over an API often from a Container Orchestrator
> * Pulling the Container Images from the Registry Server
> * Expanding decompressing and expanding the container image on disk using a Graph Driver (block, or file depending on
    driver)
> * Preparing a container mount point, typically on copy-on-write storage (again block or file depending on driver)
> * Preparing the metadata which will be passed to the Container Runtime to start the Container correctly
>   * Using some defaults from the container image (ex.ArchX86)
>   * Using user input to override defaults in the container image (ex. CMD, ENTRYPOINT)
>   * Using defaults specified by the container image (ex. SECCOM rules)
> * Calling the Container Runtime

### Container

> Containers have existed within the OS for quite a long time. A container is the runtime instantiation of a container
> image. A container is a standard Linux process typically created through a clone () system call instead of fork () or
> exec (). Also, containers are often isolated further through the use of cgroups, SELinux or AppArmor.

### Container Host

> The container host refers to the entire operating system environment running the container system—which encompasses
> the host's Linux kernel, system services, and the container runtime/engine combined. Once a container image (aka
> repository) is pulled from a Registry Server to the local container host, it is said to be in the local cache.

### Registry Server

> The remote server which holds all the shared images, such as docker.io.

### Container Orchestration

> A container orchestrator really does two things:
> 1. Dynamically schedules container workloads within a cluster of computers. This is often referred to as distributed
     computing.
> 2. Provides a standardized application definition file (kube yaml, docker compose, etc)

### Container Runtime

> A container runtime a lower level component typically used in a Container Engine but can also be used by hand for
> testing. The Open Containers Initiative (OCI) Runtime Standard reference implementation is runc.
> The container runtime is responsible for:
> * Consuming the container mount point provided by the Container Engine (can also be a plain directory for testing)
> * Consuming the container metadata provided by the Container Engine (can be a also be a manually crafted config.json
    for testing)
> * Communicating with the kernel to start containerized processes (clone system call)
> * Setting up cgroups
> * Setting up SELinux Policy
> * Setting up App Armor rules

### Image Layer

> Repositories are often referred to as images or container images, but actually they are made up of one roe more
> layers. Image layers in a repository are connected together in a parent-child relationship. Each image layer
> represents changes between itself and the parent layer.

### Repository

> When using the docker command, a repository is what is specified on the command line, not an image. This can be
> confusing, and many people refer to this as an image or a container image. In fact, the docker images sub-command is
> what is used to list the locally available repositories. Conceptually, these repositories can be thought of as
> container images, but it’s important to realize that these repositories are actually made up of layers and include
> metadata about in a file referred to as the manifest.

### Namespace

> A namespace is a tool for separating groups of repositories. On the public DockerHub, the namespace is typically the
> username of the person sharing the image, but can also be a group name, or a logical name.

### Kernel Namespace

> A kernel namespace is completely different than the namespace we are referring to when discussing Repositories and
> Registry Servers. When discussing containers, Kernel namespaces are perhaps the most important data structure, because
> they enable containers as we know them today. Kernel namespaces enable each container to have it's own mount points,
> network interfaces, user identifiers, process identifiers, etc.
>
> When you type a command in a Bash terminal and hit enter, Bash makes a request to the kernel to create a normal Linux
> process using a version of the exec () system call. A container is special because when you send a request to a
> container engine like docker, the docker daemon makes a request to the kernel to create a containerized process using
> a
> different system call called clone (). This clone () system call is special because it can create a process with its
> own
> virtual mount points, process ids, user ids, network interfaces, hostname, etc
>
> While, technically, there is no single data structure in Linux that represents a container, kernel namespaces and the
> clone () system call are as close as it comes.

### Graph Driver

---

**Reference**

* https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction#background
* https://docs.google.com/presentation/d/1OpsvPvA82HJjHN3Vm2oVrqca1FCfn0PAfxGZ2w_ZZgc/edit?slide=id.g2441f8cc8d_0_80#slide=id.g2441f8cc8d_0_80
* https://www.redhat.com/en/blog/architecting-containers-part-2-why-user-space-matters



