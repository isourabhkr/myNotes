# VPC

VPC is virtual private cloud, similar to a physical network that is used to isolate different workloads. VPC is global
resource that consists of list of regional virtual subnetworks(subnets) in data centers, all connected by a global wide
area network. VPC networks are logically isolated from each other.

## VPC Network Properties?

* VPC networks, including their routes and firewall rules are global resources.
* Subnet are regional resources.
* Subnet defines following IP address ranges:
    * IPV4 only or dual-stack subnets
    * IPV6 only
* Traffic to and from instances(VM) withing the VPC can be controlled using firewall rules. Rules are implemented at the
  VM level meaning, at VM(instance) it can be decided what to accept and what to deny, for both ingress and egress.
* Resources within the same VPC can connect to others using internal IPV4, Internal IPV6 and external IPV6, if they are
  allowed by the firewall rules.
* Instances with internal IPV4 or IPV6 address can communicate with Google APIs and Services.
* VPC Networks can be connected other VPC networks in different projects or Organisation using **VPC Network Peering**.
* VPC Networks can be connected to on premise networks using or other cloud providers using **Cloud VPN** or **Cloud
  Interconnect**.
* 