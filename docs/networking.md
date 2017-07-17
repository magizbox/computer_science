# Networking

### TCP/IP

TCP/IP is the protocol that has run the Internet for 30 years.
![](http://www.hardwaresecrets.com/wp-content/uploads/433_011.gif)

How TCP/IP works

![](http://www.billslater.com/internet/how_tcp-ip_works_.jpg)

Read More

* [Happy 30th Anniversary, Internet and TCP/IP!!!](http://www.billslater.com/internet/)

### P2P

Peer-to-peer (P2P) computing or networking is a distributed application architecture that partitions tasks or workloads between peers. Peers are equally privileged, equipotent participants in the application. They are said to form a peer-to-peer network of nodes.

![](images\p2p.png)

Peers make a portion of their resources, such as processing power, disk storage or network bandwidth, directly available to other network participants, without the need for central coordination by servers or stable hosts.[1] Peers are both suppliers and consumers of resources, in contrast to the traditional client-server model in which the consumption and supply of resources is divided. Emerging collaborative P2P systems are going beyond the era of peers doing similar things while sharing resources, and are looking for diverse peers that can bring in unique resources and capabilities to a virtual community thereby empowering it to engage in greater tasks beyond those that can be accomplished by individual peers, yet that are beneficial to all the peers.

### bridge vs NAT

When you create a new virtual machine, you have one of many options when it comes to choosing your network connectivity.  Two common options are to use either bridged networking or network address translation (NAT).  So, what exactly does that look like?  Take a look at the figure below.

![](images\bridge_vs_nat.png)

**NAT**: In this diagram, the vertical line next to the firewall represents the production network and you can see that 192.168.1.1 is the IP address of the company’s firewall that connects them to the Internet. There is also a virtual host with three virtual machines running inside it.  The big red circle represents the virtual adapter to which NAT-based virtual machines connect (172.16.1.1).  You can see that there are two such virtual machines with IP addresses of 172.16.1.2 and 172.16.1.3.  When you configure a virtual machine as using NAT, it doesn’t see the production network directly.  In fact, all traffic coming from the virtual machine will share the VM host’s IP address.  Behind the scenes, traffic from the virtual machines is routed on the virtual host and sent out via the host’s physical adapter and, eventually, to the Internet.

**bridge**: The third virtual machine (192.168.1.3) is configured in “bridged” mode which basically means that the virtual network adapter in that virtual machine is bridged to the production network and that virtual machine operates as if it exists directly on the production network.  In fact, this virtual machine won’t even be able to see the two NAT-based virtual machines since they’re on different networks.

Read more: [NAT vs. bridged network: A simple diagram](http://techgenix.com/nat-vs-bridged-network-a-simple-diagram-178/)

