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

# Overview
Here's a review of the networking flow for us to SSH into our server:

1. Our computer communicates with the server's public **Elastic IP** address.
2. The server is in a **public subnet** with a **route** to the **internet gateway**.
3. The **security group** allows **inbound** traffic on `22/tcp` from _our_ public IP address.
4. Our **SSH private key** matches the **public key** we uploaded to AWS.

## SSH 
``` bash
nc -zv YOUR.INSTANCE.IP.ADDR 22
# Connection to YOUR.INSTANCE.IP.ADDR port 22 [tcp/ssh] succeeded!
```

in `~/.ssh/config`
``` bash
Host patientping
    HostName IP_ADDR
    User ec2-user
    IdentityFile /PATH/TO/PRIVATE_KEY
```

- Modify Message of the Day
	- `echo 'Welcome, PatientPing Server Admin!' | sudo tee /etc/motd > /dev/null`
	- `tee` takes stdin and write to stdout and another source
	- Another common use — writing to privileged files with sudo:
	- ```bash 
		echo "127.0.0.1 example.com" | sudo tee -a /etc/hosts
		```
	- You can't do sudo echo "..." >> /etc/hosts because the redirect happens as your user, not root — tee solves that.


# Allow Public Web traffic
``` bash
# Get the security group ID
aws ec2 describe-security-groups --filters 'Name=group-name,Values=patientping-public' --query 'SecurityGroups[0].GroupId' --output text

# Add the inbound rule
aws ec2 authorize-security-group-ingress --group-id SG-ID --ip-permissions IpProtocol=tcp,FromPort=8080,ToPort=8080,IpRanges=[{CidrIp=0.0.0.0/0,Description="Allow web traffic for PatientPing site"}]
```

# Running Instance with custom Launch Template and AMI
``` bash
# Terminate the old instance
aws ec2 terminate-instances --instance-ids OLD-INSTANCE-ID

# Launch from template
aws ec2 run-instances --launch-template LaunchTemplateName=patientping-web-launcher --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=patientping-web-v2}]'

# Re-associate the Elastic IP
aws ec2 associate-address --instance-id NEW-INSTANCE-ID --allocation-id EIP-ALLOCATION-ID
```
