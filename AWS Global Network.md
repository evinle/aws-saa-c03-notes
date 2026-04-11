- Infrastructure - Collection of infrastructure worldwide connected by a high speed network

- 2 Types of deployments
	- AWS Regions
		- Doesn't map to physical continents
		- a creation of AWS
		- Full deployment of AWS infrastructure
		- Added frequently
	- AWS Edge Locations
		- Smaller than regions
		- Content distribution service
		- Edge computing

## Regions
- Geographically Separated - Isolated Fault Domain
- Geopolitical Separation - different governance
- Location Control - performance

- Can be referred to as 
	- Region Code: ap-southeast-2
	- Region Name: Asia Pacific (Sydney)

### Availability Zone (AZ)
- Multiple in one region
- Inside ap-southeast-2
	- ap-southeast2a
	- ap-southeast2b
	- ap-southeast2c

## Service Resilience
- Globally Resilient
	- Globally available service
	- Data replicated in multiple regions
	- IAM, Route53
- Region Resilient
	- Operate as separate services in different regions
	- Data replicated in multiple AZs
	- RDS
- AZ Resilient
	- Service only in an AZ
	- AZ fails, service fails
	- Prone to failure
