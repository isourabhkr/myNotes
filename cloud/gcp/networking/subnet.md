# Subnet

Each network contains one or more IP address ranges, which is called Subnet. Subnets in GCP are regional resources and
have IP address ranges associated with them.

A network must have at least one subnet, and there can be more then one subnet in the same region. Because Subnets are
regional object, only resources in the same region can use that particular subnet.

* When you create a virtual machine (VM) instance, you select a zone for the instance. If you don't select a network for
  the VM, the default VPC network is used, which has a subnet in every region. If you do select a network for the VM,
  you
  must select a network that contains a subnet in the selected zone's parent region.
* When you create a managed instance group, you select a zone or region, depending on the group type, and an instance
  template. The instance template defines which VPC network to use. Therefore, when you create a managed instance group,
  you must select an instance template with an appropriate configuration; the template must specify a VPC network that
  has subnets in the selected zone or region. Auto mode VPC networks always have a subnet in every region
* The process of creating a Kubernetes container cluster involves selecting a zone or region (depending on the cluster
  type), a network, and a subnet. You must select a subnet that is available in the selected zone or region.

## Types of Subnets

VPC networks supports subnets of following stack types. A single VPC network can contain any combination of these
subnets

![VPC](/asset/images/gcp/vpc_network_support_mapping.png)

Below information are required while creating a subnet:
![requirements](/asset/images/gcp/vpc_creation_requirement.png)

## Purposes of subnets

* Regular Subnets(PRIVATE): Default subnets are created to be used with VM instances. The purpose is created as **None**
  in Google Cloud Console.
    * Hybrid Subnets are regular subnets that are configured with a different routing behavior (
      --allow-cidr-routes-overlap).
* Private Service Connect subnets (PRIVATE_SERVICE_CONNECT): A subnet that is used to publish a managed service by using
  Private Service Connect.
* Proxy-only subnets (GLOBAL_MANAGED_PROXY and REGIONAL_MANAGED_PROXY): A proxy-only subnet that is used with
  Envoy-based load balancers and Secure Web Proxy.
* Private NAT subnets (PRIVATE_NAT): A subnet that is reserved for use as the source range for Private NAT.
* Peer migration subnets (PEER_MIGRATION): A subnet that you use to migrate a Shared VPC service to Private Service
  Connect.


### IPv4 subnet ranges


