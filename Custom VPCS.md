![[Pasted image 20260920181304.png]]
- Regionally Resilient - Regional Service - All AZs in the region
- Isolated network
- Nothing IN or OUT without explicit configuration
- Flexible configuration - simple or multi-tier
- Hybrid networking - other cloud & on-premises
- Default or Dedicated Tenancy


- IPv4 private CIDR blocks & public IPs
- 1 primary private CIDR block (IPv4)
	- Min /28 (16 IP)
	- Max /16 (65536 IP)
- Optional secondary CIDR blocks (max 5)
- Optional single assigned IPv6 /56 CIDR block
	- Range is allocated by AWS (can't choose)
	- Select addresses you own

# DNS 
- Provided by Route53
- VPC Base IP + 2 address
	- 10.0.0.0 -> 10.0.0.2
- `enableDnsHostnames` give instances public DNS hostnames
- `enableDnsSupport` enables DNS resolution in VPC