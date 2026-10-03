- Block Storage devices
- Physically connected to one EC2 Host
- Instances on the host can access
- Highest storage performance in AWS
- Included in the instance price
- ATTACHED AT LAUNCH, can't afterwards

- Data is lost when instance changes hosts, such as 
	- Stopping and restarting an instance
	- Current host undergoing maintenance
	- Changing instance type
- Some instance types don't support instance store volumes
- Different instance types have different types of instance store volumes

![[Pasted image 20261003211331.png]]
- D3 = 4.6 GB/s throughput
- I3 = 16 GB/s of sequential throughput
- More IOPS and throughput vs EBS