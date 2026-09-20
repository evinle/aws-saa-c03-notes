# Router and Route Tables
- Every VPC has a VPC Router - highly available
- Network + 1 address in every subnet
- Controlled by route tables - each subnet has one
- VPC has a Main route table - subnet default
- ![[Pasted image 20260920223620.png]]
- 0.0.0.0 is the default route in the route table (catch-all)
- All route tables have at least 1 route - local route, cannot be edited
	- Matches VPC CIDR range
	- Lets route table know local traffic that can be delivered locally
	- If IPv6 is enabled, RT will also have that
	- Local routes always take priority
- Route tables are attached to 0+ subnets
- Subnets can have either the Main route table from the vpc or a custom one
- Route tables controls what happens to the data when it leaves the subnet

# Internet Gateway (IGW)
- Regionally resilient, attached to a VPC
- VPC can have 0 to 1 IGW
	- IGW can only be attached to 1 VPC at a time
	- Available in all AZs the VPC uses
- Runs from within the AWS Public Zone
- Allows services with public IPv4 or IPv6 addresses to be reached from the internet or to AWS Public Zone (S3, SQS, SNS)
- Managed - AWS handles performance
- ![[Pasted image 20260920224654.png]]

# IPv4 Addressing in VPC
- Public IP addressing is fake in VPC, the public IPv4 address is actually assigned at the IGW level, not directly tied to the instance of something like EC2. 
- The EC2 instance would only see the private IP address assigned from the private subnet
- ![[Pasted image 20260920225210.png]]
- Public address never touches the instance
- IPv6 case does have the 

# Bastion Host / Jumpbox
- instance in a public subnet
- Incoming management connections arrive there
- Then access internal VPC resources
- Management point/access point
- Often the only way to IN to a VPC