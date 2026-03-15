# What is networking?

Networking facilitates communication between two or more devices, nowadays even with one device(while running multiple
VMs or containers).

## What are protocols?

## Half Vs Full Duplex Communication

Half Duplex: Can send and receive data, but not at the same time.
Full Duplex: Can send and receive data simultaneously.

## Network Transmission types

How devices communicate in a network:

1. Unicast (1:1)
2. Multicast (1: Multicast group)
3. Broadcast (1:All)

## Network Topologies

### Wired Network Topology

- Bus: All devices connected to a single coaxial network cable.Only one end device can be active on the network at a
  time.

- Ring: Each device in the network is connected with two other devices, making a circle. Each device also works as a
  repeater,
  where it has to forward the data not intended for itself. Usually have to have 2 NICs to connect to two different
  devices.

- Star: Most used wired network topology. A single switch is connected to all the devices in the network. And hence
  switch also
  being the single point of failure.

- Mesh: Each device is connected to every other device by separate cabling.
    - Partial Mesh
    - Full Mesh

### Wireless Network Topology

- Adhoc: Peer to peer wireless network where no access point(WAP) infrastructure exits.

- Infrastructure: One wireless network access point which connects to other devices in the network wirelessly at the
  same time connecting to the wired network.

- Mesh: More than one wireless access point, and these wireless access points are connected to each other. Providing
  extended wireless coverage.

![Network-Topology](/asset/images/networking/network_topology.png)
