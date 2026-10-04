- Used to launch EC2 instance
- AWS or Community provided
- Marketplace (includes commercial software)
- Regional, with unique ID
	- ami-32a3782bd82
- Permissions - Public, Your account, specific accounts
- Can create AMI from EC2 instance

# AMI lifecycle
- Launch, Configure, Create Image, Launch
- Creating an AMI from an instance with EBS = Block Device Mapping of snapshot of EBS state as well, referenced in AMI
	-New EBS are created as well
 - ![[Pasted image 20261004133148.png]]

# Exam Powerup
- AMI = One Region, only works in one region
- AMI Baking = creating an AMI from configured instance + app
- AMI cannot be edited = launch instance, update config, make new AMI
- AMIs can be copied between regions
- By default, only available on your account
