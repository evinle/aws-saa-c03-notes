- VPC CIDR ranges
- Deciding in advance = critically important - not easy to change later
- Decision
	- What size should the VPC be
	- Any networks we can't use?
	- VPC's, Cloud, On-premise, Partners and Vendors - occupied ranges
	- VPC Structure - Tiers & resiliency (AZ)
- ![[Pasted image 20260920172214.png]]
- ![[Pasted image 20260920172400.png]]

- VPC - smallest /28 (16 IP), biggest /16 (65536 IP)
- Avoid common ranges - avoid future issues of overlap
- Think about the highest number of possible regions and then add a few
- 2 ranges to be used in each region in each aws account
- ![[Pasted image 20260920172854.png]]


# VPC Sizing

![[Pasted image 20260920173028.png]]
- Considerations
	- How many subnets
	- How many IPs total?
- Good rule of thumb 
	- 3 + 1 spare AZs
	- 3 + 1 spare tiers (Web, App, Db) 
	- 16 subnets, one per az per tier
	- starting at /16, subnets will be each /20
		- /17 -> /21
		- /18 -> /22
		- etc.
		- every bit pushed up, you get 2^n subnets