- A set of processes - remap src or dst IPs for public internet traffic
- Does IP masquerading - hide CIDR blocks behind 1 IP
- Gives Private CIDR range outgoing ONLY internet access

2 ways to provide NAT
- EC2 or NAT Gateway (within a VPC)

# How it works
- Private subnet has route table that points to NAT Gateway in the public VPC (which has access to internet through IGW)
- NAT Gateway forwards to IGW, at this point, still no public IP
- IGW swaps IP again for its public internet address, then reach out to other server
![[Pasted image 20260922225949.png]]

- NAT gateways use elastic IPs
- AZ resilient Service, unlike IGW which is regionally resilient
- Managed, scales to 45 gbps
- Billed by hours + data processing charge (per GB per processed data)

# NAT Instance 
- In an EC2 instance
- By default, drops traffic whose source or destination is not the EC2 instance itself
	- Can disable `Source/Destination Checks` to not drop them
- Not preferrable, except in specific scenarios
	- Cheaper, port forwarding, bastion host
	- NAT gateways cannot use SG, only NACL

# IPv6
- Doesn't require NAT
- By default can just work with IGW
- Down the line, we will learn about Egress-Only Internet Gateway - Outbound only, IPv6 only