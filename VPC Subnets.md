- Blue = private subnets
- Green = public subnets
- ![[Pasted image 20260920213649.png]]
- subnetwork of a vpc - within a particular AZ
- 1 subnet -> 1 AZ
- 1 AZ -> 0+ subnets
- IPv4 CIDR is a subset of the VPC CIDR
- IPv6 CIDR /64 subset of the /56 VPC
- subnets can communicate with other subnets in the VPC

# Subnet IP Adressing
- Reserved IP address - 5 in total
- 10.16.16.0/20 (10.16.16.0 -> 10.16.31.255)
- Network address (10.16.16.0)
- Network + 1 (10.16.16.1) - VPC Router
- Network + 2 (10.16.16.2) - Reserved (DNS)
- Network + 3 (10.16.16.3) - Reserved Future Use
- Broadcast Address 10.16.31.255 (Last IP in subnet)

# DHCP Options Set
- DHCP Options Set applied to VPC, flows through to subnet
	- DNS servers
	- MTP servers
	- NetBIOS servers
- Can create options set, but can't edit
- Can configure (at a subnet level)
	- Whether resources are assigned public IPv4 
	- Whether resources are assigned IPv6 