# Prerequisite
- First we need to set up SSH keys in our VPC
- `ssh-keygen -t ed25519 -C "patientping-key" -f ~/.ssh/patientping-key`
	- `-C`: comment
	- `-f`: output keyfile
	- `-t`:   (key type - ed25519 default) dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa
- Then we can import the key pair into aws EC2
	- `aws ec2 import-key-pair --key-name "patientping-key" --public-key-material fileb://$HOME/.ssh/patientping-key.pub`
- Check 
	- `aws ec2 describe-key-pairs`

# Launching
- Will mainly need the AMI - Amazon Machine Image
- Contains base software
	- Could just be an OS like linux or windows server
- Then an Instance Type 
	- The actual hardware - memory cpu storage etc.
- Security Group - SG = Firewall

# Public IPs
- Will be using EIP - Elastic IP
- Costs the same as automatic addressing
- Will get assigned from a pool of addresses in your region
- `aws ec2 allocate-address --domain vpc`
- `aws ec2 associate-address --instance-id INSTANCE-ID --allocation-id ALLOCATION-ID`
- `aws ec2 disassociate-address --association-id eipassoc-1234567890abcdef0`
- `aws ec2 release-address --allocation-id eipalloc-1234567890abcdef0`
- `aws ec2 describe-addresses`
> [!Creating through CLI]- 
Why should I specify the **--domain vpc** flag when creating from the cli?
In the context of modern AWS, specifying --domain vpc tells AWS to allocate the Elastic IP for use within a Virtual Private Cloud (VPC) rather than the older, legacy "EC2-Classic" network.
Here is why that flag is significant: 
#1. Modern Standard
Most AWS accounts created after 2013 only support VPC. EC2-Classic was the original flat network where all instances shared a single network space. Since EC2-Classic has been retired in almost all regions, using --domain vpc ensures your IP is compatible with the modern VPC infrastructure where your patientping-web instance lives.
#2. Feature Availability
Elastic IPs allocated for a VPC have features that Classic ones didn't, such as:
The ability to associate the IP with a specific Network Interface (ENI) rather than just an Instance ID.
The ability to move the IP between instances in different subnets within the same VPC. #3. API Consistency
While some regions might default to VPC if you omit the flag, explicitly defining it in your scripts or CLI commands prevents errors. If you tried to associate a "Classic" IP (if your account even allowed creating one) with a VPC instance, the command would fail because the address "scopes" don't match.
In short, it’s a way of saying: "Give me an address that works with my modern, private virtual network."

# Security Group
- To create rules for inbound and outbound traffic
- Right now hardcoding to the current IP of the machine I'm playing with
	- Allows SSH traffic through TCP:22 from my IP address
- ![[Pasted image 20260405103930.png]]
``` bash
# Create a security group
aws ec2 create-security-group --group-name NAME --description DESCRIPTION --vpc-id VPC-ID

# Add an inbound rule
aws ec2 authorize-security-group-ingress --group-id SG-ID --ip-permissions IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges=[{CidrIp=YOUR-IP/32,Description=DESCRIPTION}]

# Attach to an instance
aws ec2 modify-instance-attribute --instance-id INSTANCE-ID --groups SG-ID
```
