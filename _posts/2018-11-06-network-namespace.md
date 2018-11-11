---
title: Network Namespace
layout: post
tag:
- Linux
- Networking
category: blog
author: Anran Zhou
date: '2018-11-06 16:02:14'
---

## 1. Basics
* Create and Show

|Function|Command|
|:---:|:---:|
|Create a network namespace|ip netns add testns1|
|Get list of network namespaces|ip netns list|
|Accessing NS|host shell: ip netns exec < name of NS > {shell} |
||netns shell: ip netns exec < name of NS > bash|

* Add an interface in the namespace
	1. Create a veth pair interface
		```
			ip link add testif0 type veth peer name testif1
		```
		
	2. Add interface to a namespace
		```
			ip link set testif0 netns testns1
			ip link set testif1 netns testns2
		```
		
	3. Configure IP of the namespaces interfaces.
		```
			ip netns exec netns1 ifconfig testif0 10.1.1.1/24 up
			ip netns exec netns2 ifconfig testif1 10.1.1.2/24 up
		```
		
	4. Verify routing table in each name space using the command
		```
			ip netns exec < Name of NS > ip route show
		```
		
	Verify: Ping from one namespace to the other namespace.
	
## 2. Single NS: Internet Connectivity
Tasks:
* Create a network NS.
* Ping from network NS to outside using NAT

Steps:
1. Create a veth pair interface in the host
2. Attach an host interface to netns
3. Configure Interfaces' IP addresses
	```
		 ip addr add 1.1.1.1/24 dev veth12 up
		 ip netns exec NS1 ip addr add 1.1.1.1/24 dev veth11
	```
4. Default gateway con figuration at the netns
	```
		 ip netns exec NS1 ip route add default via 1.1.1.1
	```
5. NAT rule for netns at the host
	```
		// define
		iptables -t nat -A POSTROUTING -s 1.1.1.0/24 ! -d 1.1.1.0/24 -j MASQUERADE
		// verify
		iptables -t nat -L
	```
6. Verification: Connectivity to hypervisor
	 ```
		 ping 1.1.1.1
	```
7. Configure DNS
	Create a resolv.conf file in the directory /etc/netns/NS1 and add 8.8.8.8 as nameserver

8. Verification: Connectivity to Internet
	 ```
		 ping www.google.com
	```