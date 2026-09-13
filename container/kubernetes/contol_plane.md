# Control Plane

The control plane is a collection of system services that implement the brains of Kubernetes. It exposes the API,
schedules apps, implements self-healing, manages scaling operations, and more.

![Control Plane](/asset/images/kubernetes/control_plane.png)

## Control Plane Components

Each control plane has below components

![Cluster Components](/asset/images/kubernetes/cluster_components.png)

### The API server (kube-apiserver)

The API server (also know as kube-apiserver) works as the gateway for k8s and all commands and requests go through it.
Even internal control plane services communicate with each other via the API server.

It exposes a RESTful API over HTTPS, and all requests are subject to authentication and authorization.

### The cluster store (etcd)

The cluster store holds the desired state of all applications and cluster components, and it’s the only stateful part of
the control plane.

It’s based on the `etcd` distributed database, and most Kubernetes clusters run an etcd replica on every control plane
node for HA. However, large clusters that experience a high rate of change may run a separate etcd cluster for better
performance.

> Regarding availability, etcd prefers an odd number of replicas to help avoid split brain conditions. This is where
> replicas experience communication issues and cannot be sure if they have a quorum (majority).

<details>

<summary>Split brain</summary>
Split brain conditions in computing (and Kubernetes clusters) refer to a situation where a cluster of servers (
nodes) loses communication between two or more groups, so each group incorrectly believes the others are offline. As a
result, multiple groups may act as the primary/leader at the same time, leading to conflicting operations and
potentially data corruption or inconsistent states across the cluster.

Below shows two etcd configurations experiencing a network partition error. Cluster A on the left has four nodes and is
experiencing a split brain with two nodes on either side and neither having a majority. Cluster B on the right only has
three nodes but is not experiencing a split-brain as Node A knows it does not have a majority, whereas Node B and Node C
know they do.

![Network partition](/asset/images/kubernetes/network_partition.png)

If a split-brain occurs, etcd goes into read-only mode preventing updates to the cluster. User applications will
continue working, but Kubernetes won’t be able to scale or update them.

As with all distributed databases, consistency of writes is vital. For example, multiple writes from different sources
to the same can cause corruption. etcd uses the RAFT consensus algorithm to prevent this from happening.

</details>

### Controllers and the Controller manager

Kubernetes uses controllers to implement a lot of the cluster intelligence. Logically, each controller is a separate
process, but to reduce complexity, they are all compiled into a single binary and run in a single process. Each
controller runs as a process on the control plane in background, and some of the more common ones include:

* Node controller: Responsible for noticing and responding when nodes go down.
* Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to
  completion.
* EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
* ServiceAccount controller: Create default ServiceAccounts for new namespaces.

> All the controllers run as background watch loops, reconciling observed state with desired state.

In a nutshell controllers ensure the cluster runs what you asked it to run. For example, if you ask for three replicas
of an app, a controller will ensure you have three healthy replicas and take appropriate actions if you don’t.


> Kubernetes also runs a controller manager that is responsible for spawning and managing the individual controllers.

![Controller Managers with Controllers](/asset/images/kubernetes/controller_manager.png)

### The Scheduler (kube-scheduler)

The scheduler watches the API server for new work tasks and assigns them to healthy worker nodes. In other words,
chooses the best node for a newly created pod.

Factors taken into account for scheduling decisions include: individual and collective resource requirements,
hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload
interference, and deadlines.

### cloud-control-manager

A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you
link your cluster into your cloud provider's API, and separates out the components that interact with that cloud
platform from components that only interact with your cluster
