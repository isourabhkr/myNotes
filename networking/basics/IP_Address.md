# What is an IP Address?

An IP address is a Network layer numeric address. It's an identifier for a computer or a device on a network. Every
device has to have an IP address for communication purposes. It's also a logical address, it can change for a device,
i.e. the IP address can change and it's not assigned uniquely like MAC address on a device level that can not be
changed. Used for WAN communication.

It basically consists of two parts:

1. Network address
2. Host address

There basically two types of IP address protocols:

1. IPV4: 32 bit numeric address written as four numbers separated by periods. Ex: 192.1.2.56, 9.9.9.9.

   Each section **192**.1.2.56 like 192 here is called octet and can range from 0 - 255. Hence, the IPV4 can have
   4,294,967,296 unique IP addresses.

2. IPV6: 128-bit hexadecimal address, written as hexadecimal numbers which consists of both numbers and alphabets. These
   are 16 bit sets separated by colons(:). Ex: 76DC:45AD:3B2A:863C:91BC:21AC:1345:7856

   Here each hexadecimal character represents 4 bits making 8 * 4 * 8 = 128 bits address.
   IPV6 is capable of providing 340 un decillion addresses.

Two kinds of IP address:

Public Address and Private Address

* Public address: Public IP address are registered on the internet and also unique thought the world.

* Private address: Not registered on the interned and hence anc not connected directly to the internet. For a device in
  the private internet having a private IP address needs IP translation to a public address to connect to internet.

The private IP address must be translated to the public IP addresses we have been given by the internet providers. And
the service which does the translation is called NAT (Network Address Translation), and NAT comes pre-installed in the
Routers. It translate from private to public IP when the internal device wants to connect to internet. As well as public
to private IP translation when a device from internet trying to connect a device in a private network.

In a home setup the router provided by the Internet provider acts as the gateway to the public internet. The router has
a service called DHCP which assigns the private IPs to the devices in the internal network.

There are basically 3 different ranges in a private IP address pool.

Class A, B C as shown in the image below.

![Private IP Ranges](/asset/images/networking/private_ip_ranges.png)

---

## Links

* <https://www.youtube.com/watch?v=po8ZFG0Xc4Q>
