- Infrastructure-as-a-Service - IAAS
- Provides Virtual Machines - Instances
	- OS configured in a certain way with certain set of allocated resources
- Private AWS service - uses VPC networking
	- Launched inside a subnet
	- By default private, unless used in default VPC
- AZ Resilient - AZ fails - instance fails
- Configure Resources - Capabilities - storage, gpu, networking
- On Demand billing - Per second / per hour
	- Running, cpu, memory
	- Storage, EC2 local on host storage/EBS
	- Commercial Software extra?

## Lifecycle
- Running 
		- While running, you are charged for
			- CPU
			- Memory
			- Disk
			- Networking
- Stopped (temp shutdown)
		- While stopped, you are only charged for storage
		- Storage for stopped instance still remains, so you're still charged
- Terminated - one way
		- You don't pay for anything
		- Also terminates storage 
	![[Pasted image 20260411144230.png]]

## AMI
- EC2 instance image
- w

