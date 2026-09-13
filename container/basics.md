# Why container?

The history of containers goes long back and the problem it solves are related to better resource utilization, better deployment, better fail over strategies, easy scalability, better practices of development.

Usually in the initial days, to run an application we had to buy servers (nothing but a bigger computer). This caused problems of under-utilizing the available resources, because of the very nature of humans, we buy more then what we need(buying bigger servers that's actually needed). To overcome this, we started to run multiple applications on the same server. This does gave us a better resource utilization but came at a cost of highly unmanageable systems. Basically, different apps have very different dependencies and maintaining the dependency without really having an isolation was not pragmatic.

To solve this problem, virtual machines evolved and governed the markets for long. Virtual machines in the core is a virtual computer running on the Hypervisor that's running on the Host OS .i.e, allowing multiple copies of OS to run on one single hardware.
Benefits of VMs

1. Maximum resource utilization.
2. Absolute isolation of running environment.
3. Can run multiple OSs.

Problem with VMs

1. Overhead of Hypervisor and OS on each runnable environment. Which results in loss of resources to not doing actual task, but to maintain the an executable environment.

Finally comes containers, though containers always existed in OS, Docker was the major project, which brought application containerization into reality.
Application containers share the host OS through a software layer(in case of docker, docker engine). Hence, an application container would only need all the libraries needed to run an application, and the light weight software layer sharing the Host OS.
Benefits of application containers:

1. Very light weight software layer.
2. Very light weight application containers.
3. Can spin up application very fast.

Problems with Containers:

1. As all the applications are sharing same host OS, security is a concern in some very confidential applications.

Difference between Hypervisors and Container
Hypervisors:

* Allow an operating system to run independently from the underlying hardware through the use of virtual machines.
* Share virtual computing, storage and memory resources.
* Can run multiple operating systems on top of one server (bare-metal hypervisor) or installed on top of one standard operating system and isolated from it (hosted hypervisor).

Containers:

* Allow applications to run independently of an operating system. 
* Can run on any operating system—all they need is a container engine to run. 
* Are extremely portable since in a container, an application has everything it needs to run.

----
Reference:

* <https://www.vmware.com/topics/glossary/content/hypervisor.html>
* <https://www.redhat.com/en/topics/containers/whats-a-linux-container#:~:text=A%20Linux%C2%AE%20container%20is,testing%2C%20and%20finally%20to%20production.>
* <https://www.section.io/engineering-education/lxc-vs-docker-what-is-the-difference-and-why-docker-is-better/#:~:text=What%20is%20the%20major%20difference,multi%2Dpurpose%20operating%20system%20virtualization.>
* <https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction#background>
