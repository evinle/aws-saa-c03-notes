- Everything is built on top of a VPC (Virtual Private Cloud)
- You can then configure

# Region & Availability Zones
- Each region is in a different geography
- Choose region that is closer to have a faster connection
- Configure the region by 
	- `aws configure set region <REGION>`
	- OR from the web interface
	- top right and select region
# Subnets
- Subnets use CIDR (classless inter domain routing) to determine what range is available in that subnet
	- `10.0.1.0/24` 
		32 - 24 = 8 bits left for the subnet
		2^8 = 256 addresses from 0 to 255
- Can set Subnets in the "Subnets" tab in the VPC console
- Check subnets by running
	- `aws ec2 describe-subnets`

# IGW & RT- Internet Gateway & Route Table
- Internet Gateway is the gateway to the internet
- Routes & Route Table tells the subnets where to reach for the internet - a default catch all for addresses, if no private address found
- You can then assign the 
	- `aws ec2 describe-internet-gateways`
	- `aws ec2 describe-route-tables`
	- `aws ec2 create-internet-gateway --tag-specifications 'ResourceType=internet-gateway,Tags=[{Key=Name,Value=patientping-igw}]'`
	- `aws ec2 attach-internet-gateway --internet-gateway-id igw-05f123456789abcde --vpc-id vpc-0a1b2c3d4e5f6g7h8`
