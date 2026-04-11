- Virtual Network inside AWS
- Within 1 account and 1 region
	- Regionally resilient
- Isolated from public and other VPCs by default

## VPC types
- Default VPC
	- Max 1 per region
	- Preconfigured
	- Less Flexible
		- 172.31.0.0/16 CIDR
		- Subnets in each AZ
		- ![[Pasted image 20260411130131.png]]
	- Could have 0 to 1 defaults - removed and recreated
	- Internet Gateway (IGW), Security Group (SG) & Network Access Control List (NACL)
	- Subnets assigned public IPv4 addresses

- Custom VPCs
	- Many
	- Most configurable