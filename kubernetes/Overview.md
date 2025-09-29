# What is Kubernetes?

Kubernetes is an application orchestrator(Orchestrator is jargon for a system that deploys and manages applications.),
that takes care of the underline infrastructure. It manages different resources and takes care of the overall resource
management.

## Components

### Kubernetes: Cluster

Kubernetes cluster is one or more nodes providing CPU, memory, and other re-sources for application use.

It supports two types of nodes:

* **Control Plane Node**: Implements the K8S intelligence and every cluster needs at least once. There can be more than
  one
  control plane node.

> Note:
> * Every control plane node runs every control plane service. These include the API server, the scheduler, and the
    > controllers that implement cloud-native features such as self-healing, autoscaling, and rollouts.
> * Control plane nodes must be Linux, but workers can be Linux or Windows.
> * Kubernetes cluster can have a mix of Linux and Windows worker nodes, and Kubernetes is intelligent enough to
    schedule apps to the correct nodes.

* **Worker node**: Where the business application runs.

### Kubernetes: Orchestrator

That takes care deploying an application to different nodes, take an example of an application running in multiple
containers and need to be updated. It is capable of fixing things, for example when a machine shuts down abruptly
without a warning to replace the same with a healthy node.


