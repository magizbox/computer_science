## Linux

Linux  is a Unix-like computer operating system assembled under the model of free and open-source software development and distribution. The defining component of Linux is the Linux kernel, an operating system kernel first released on September 17, 1991 by Linus Torvalds. The Free Software Foundation uses the name GNU/Linux to describe the operating system, which has led to some controversy.

## Networking

### [ping](http://www.computerhope.com/unix/uping.htm)

*send ICMP ECHO_REQUEST to network hosts*

ping uses the ICMP protocol's mandatory ECHO_REQUEST datagram to elicit an ICMP ECHO_RESPONSE from a host or gateway.   ECHO_REQUEST  datagrams (''pings'')  have  an  IP and ICMP header, followed by a struct timeval and then an arbitrary number of ``pad'' bytes  used  to  fill  out  the packet.

```
$ ping google.com
PING google.com (74.125.200.102) 56(84) bytes of data.
64 bytes from plus.google.com (74.125.200.102): icmp_req=1 ttl=128 time=172 ms
64 bytes from plus.google.com (74.125.200.102): icmp_req=2 ttl=128 time=164 ms
64 bytes from plus.google.com (74.125.200.102): icmp_req=4 ttl=128 time=165 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3013ms
rtt min/avg/max/mdev = 164.618/167.289/172.010/3.364 ms

# Wait for 5 seconds before sending the next packet.
$ ping -i 5 google.com
# Wait 0.1 seconds before sending the next packet.
$ ping -i 0.1 google.com

# Send N packets and stop
$ ping -c 4 google.com
```

### [ifconfig](http://www.computerhope.com/unix/uifconfi.htm)

*configure a network interface*

Ifconfig  is  used to configure the kernel-resident network interfaces. It is used at boot time to set up interfaces as necessary.  After that, it  is  usually  only  needed  when  debugging or when system tuning is needed.

```
$ ifconfig

eth0      Link encap:Ethernet  HWaddr 09:00:12:90:e3:e5  
          inet addr:192.168.1.29 Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe70:e3f5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:54071 errors:1 dropped:0 overruns:0 frame:0
          TX packets:48515 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:22009423 (20.9 MiB)  TX bytes:25690847 (24.5 MiB)
          Interrupt:10 Base address:0xd020 

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:83 errors:0 dropped:0 overruns:0 frame:0
          TX packets:83 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:7766 (7.5 KiB)  TX bytes:7766 (7.5 KiB)

wlan0     Link encap:Ethernet  HWaddr 58:a2:c2:93:27:36  
          inet addr:192.168.1.64  Bcast:192.168.2.255  Mask:255.255.255.0
          inet6 addr: fe80::6aa3:c4ff:fe93:4746/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:436968 errors:0 dropped:0 overruns:0 frame:0
          TX packets:364103 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:115886055 (110.5 MiB)  TX bytes:83286188 (79.4 MiB)
```

### [tcpdump](http://www.computerhope.com/unix/tcpdump.htm)

*dump traffic on a network*

Tcpdump prints out a description of the contents of packets on a network interface that match the boolean expression specified on the command line. It can also be run with the -w flag, which causes it to save the packet data to a file for later analysis, and/or with the -r flag, which causes it to read from a saved packet file rather than to read packets from a network interface.

```
$ tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
15:29:50.659457 IP de94d0dc3aae.57956 > 10.0.2.3.domain: 9300+ A? google.com. (28)
15:29:50.663588 IP 10.0.2.3.domain > de94d0dc3aae.57956: 9300 1/0/0 A 216.58.221.110 (44)
15:29:50.663929 IP de94d0dc3aae > hkg07s01-in-f110.1e100.net: ICMP echo request, id 111, seq 1, length 64
15:29:50.700673 IP hkg07s01-in-f110.1e100.net > de94d0dc3aae: ICMP echo reply, id 111, seq 1, length 64
15:29:50.700935 IP de94d0dc3aae.45017 > 10.0.2.3.domain: 7464+ PTR? 110.221.58.216.in-addr.arpa. (45)
15:29:50.704494 IP 10.0.2.3.domain > de94d0dc3aae.45017: 7464 2/0/0 PTR hkg07s01 -in-f110.1e100.net., PTR hkg07s01-in-f14.1e100.net. (115)
15:29:51.299761 IP de94d0dc3aae.51092 > 10.0.2.3.domain: 21551+ PTR? 3.2.0.10.in -addr.arpa. (39)
15:29:51.304756 IP 10.0.2.3.domain > de94d0dc3aae.51092: 21551 NXDomain 0/1/0 (88)
15:29:51.305129 IP de94d0dc3aae.43261 > 10.0.2.3.domain: 50964+ PTR? 110.221.58.216.in-addr.arpa. (45)
15:29:51.306953 IP 10.0.2.3.domain > de94d0dc3aae.43261: 50964 2/0/0 PTR hkg07s0
1-in-f110.1e100.net., PTR hkg07s01-in-f14.1e100.net. (124)
15:29:51.666092 IP de94d0dc3aae > hkg07s01-in-f110.1e100.net: ICMP echo request, id 111, seq 2, length 64
15:29:51.704405 IP hkg07s01-in-f110.1e100.net > de94d0dc3aae: ICMP echo reply, i d 111, seq 2, length 64
15:29:52.667729 IP de94d0dc3aae > hkg07s01-in-f110.1e100.net: ICMP echo request, id 111, seq 3, length 64
15:29:52.703594 IP hkg07s01-in-f110.1e100.net > de94d0dc3aae: ICMP echo reply, i d 111, seq 3, length 64
15:29:53.668805 IP de94d0dc3aae > hkg07s01-in-f110.1e100.net: ICMP echo request, id 111, seq 4, length 64
15:29:53.703928 IP hkg07s01-in-f110.1e100.net > de94d0dc3aae: ICMP echo reply, i d 111, seq 4, length 64
 id 111, seq 5, length 64dc3aae > hkg07s01-in-f110.1e100.net: ICMP echo request,
15:29:54.706720 IP hkg07s01-in-f110.1e100.net > de94d0dc3aae: ICMP echo reply, i d 111, seq 5, length 64 id 111, seq 6, length 64dc3aae > hkg07s01-in-f110.1e100.net: ICMP echo request,
15:29:55.711018 IP hkg07s01-in-f110.1e100.net > de94d0dc3aae: ICMP echo reply, i d 111, seq 6, length 64

# Capture packets from a particular ethernet interface
$ tcpdump -i eth1

# Capture only N number of packets
$ tcpdump -c 2 -i eth0

# Display Captured Packets in ASCII
$ tcpdump -A -i eth0
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes
14:34:50.913995 IP valh4.lell.net.ssh > yy.domain.innetbcp.net.11006: P 1457239478:1457239594(116) ack 1561461262 win 63652
E.....@.@..]..i...9...*.V...]...P....h....E...>{..U=...g.
......G..7\+KA....A...L.
14:34:51.423640 IP valh4.lell.net.ssh > yy.domain.innetbcp.net.11006: P 116:232(116) ack 1 win 63652
E.....@.@..\..i...9...*.V..*]...P....h....7......X..!....Im.S.g.u:*..O&....^#Ba...
E..(R.@.|.....9...i.*...]...V..*P..OWp........

# Display Captured Packets in HEX and ASCII
$ tcpdump -XX -i eth0

# Capture the packets and write into a file
$ tcpdump -w 08232010.pcap -i eth0

# Reading the packets from a saved file
$ tcpdump -tttt -r data.pcap

# Capture packets with IP address 
$ tcpdump -n -i eth0
15:01:35.170763 IP 10.0.19.121.52497 > 11.154.12.121.ssh: P 105:157(52) ack 18060 win 16549
15:01:35.170776 IP 11.154.12.121.ssh > 10.0.19.121.52497: P 23988:24136(148) ack 157 win 113
15:01:35.170894 IP 11.154.12.121.ssh > 10.0.19.121.52497: P 24136:24380(244) ack 157 win 113

# Capture packets with proper readable timestamp
$ tcpdump -n -tttt -i eth0

2010-08-22 15:10:39.162830 IP 10.0.19.121.52497 > 11.154.12.121.ssh: . ack 49800 win 16390
2010-08-22 15:10:39.162833 IP 10.0.19.121.52497 > 11.154.12.121.ssh: . ack 50288 win 16660
2010-08-22 15:10:39.162867 IP 10.0.19.121.52497 > 11.154.12.121.ssh: . ack 50584 win 16586

# Read packets longer than N bytes
$ tcpdump -w g_1024.pcap greater 1024

# Receive only the packets of a specific protocol type
$ tcpdump -i eth0 arp

# Receive packets flows on a particular port 
$ tcpdump -i eth0 port 22
19:44:44.934459 IP valh4.lell.net.ssh > zz.domain.innetbcp.net.63897: P 18932:19096(164) ack 105 win 71
19:44:44.934533 IP valh4.lell.net.ssh > zz.domain.innetbcp.net.63897: P 19096:19260(164) ack 105 win 71
19:44:44.934612 IP valh4.lell.net.ssh > zz.domain.innetbcp.net.63897: P 19260:19424(164) ack 105 win 71

# Capture packets for particular destination IP and Port
$ tcpdump -w xpackets.pcap -i eth0 dst 10.181.140.216 and port 22
```

### [netstat](http://www.computerhope.com/unix/unetstat.htm)

* Print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships*

Netstat prints information about the Linux networking subsystem.  The type of information printed is controlled by the first argument 

```
$ netstat
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
Active UNIX domain sockets (w/o servers)
Proto RefCnt Flags       Type       State         I-Node   Path

# list all ports
$ netstat -a | more
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 localhost:30037         *:*                     LISTEN
udp        0      0 *:bootpc                *:*                                

Active UNIX domain sockets (servers and established)
Proto RefCnt Flags       Type       State         I-Node   Path
unix  2      [ ACC ]     STREAM     LISTENING     6135     /tmp/.X11-unix/X0
unix  2      [ ACC ]     STREAM     LISTENING     5140     /var/run/acpid.socket

# list all tcp ports
$ netstat -at

# list all udp ports
$ netstat -au

# List Sockets which are in Listening State
$ netstat -l
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 localhost:ipp           *:*                     LISTEN
tcp6       0      0 localhost:ipp           [::]:*                  LISTEN
udp        0      0 *:49119                 *:*

# List only listening TCP Ports using netstat -lt
$ netstat -lt

# List only listening UDP Ports using netstat -lu
$ netstat -lu

# List only the listening UNIX Ports using netstat -lx
$ netstat -lx

# Display the kernel routing information
$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
192.168.1.0     *               255.255.255.0   U         0 0          0 eth2
link-local      *               255.255.0.0     U         0 0          0 eth2
default         192.168.1.1     0.0.0.0         UG        0 0          0 eth2

# Note: Use netstat -rn to display routes in numeric format
# without resolving for host-names.

# Show the list of network interfaces
$ netstat -i
```

### hostfile

The computer file hosts is an operating system file that maps hostnames to IP addresses. It is a plain text file. Originally a file named HOSTS.TXT was manually maintained and made available via file sharing by Stanford Research Institute for the ARPANET membership, containing the hostnames and address of hosts as contributed for inclusion by member organizations

**File content**

The hosts file contains lines of text consisting of an IP address in the first text field followed by one or more host names. Each field is separated by white space – tabs are often preferred for historical reasons, but spaces are also used. Comment lines may be included; they are indicated by a hash character (#) in the first position of such lines. Entirely blank lines in the file are ignored. For example, a typical hosts file may contain the following:

```
127.0.0.1  localhost loopback
::1        localhost
```

**Location in the file system**

|    Operating System    |         Versions          |                      Location                      |
|------------------------|---------------------------|----------------------------------------------------|
| Unix, Unix-like, POSIX |                           | /etc/hosts                                         |
| Microsoft Windows      | 3.1                       | %WinDir%\HOSTS                                     |
|                        | 95, 98, ME                | %WinDir%\hosts                                     |
|                        | NT, 2000, XP, 2003, Vista | %SystemRoot%\System32\drivers\etc\hosts            |
|                        | 2008, 7, 2012, 8, 10      |                                                    |
| Apple Macintosh        | 9 and earlier             | Preferences or System folder                       |
|                        | Mac OS X 10.0–10.1.5      | (Added through NetInfo or niload)                  |
|                        | Mac OS X 10.2 and newer   | /etc/hosts (a symbolic link to /private/etc/hosts) |


**References**

* [Complete Linux Networking Tutorial](https://www.youtube.com/watch?v=fHgk7aDGn_4)
* [Linux Networking Tutorial for System Admins w/Subtitles](https://www.youtube.com/playlist?list=PLYmlEoSHldN498gmB-W-z3PEN5bevM53B)
* [Linux Networking Basics](https://www.youtube.com/watch?v=51tX4XFNGqY&list=PLD77wXPYdVJIf2OaienlLgLzibW_LrKx2)
* [Packet Analyzer: 15 TCPDUMP Command Examples](http://www.thegeekstuff.com/2010/08/tcpdump-command-examples/)