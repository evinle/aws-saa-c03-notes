3 main jobs
- Metrics - public service, in AWS, on Premises, within other clouds
	- CPU, memory, storage, visitors to site
	- Some metrics are gathered natively
	- Some require CloudWatch Agents
- CloudWatch Logs 
	- logging data
- CloudWatch Events
- ![[Pasted image 20260425170626.png]]


## Namespace
- Container for monitoring data
- Namespace name can be almost anything, except
	- All AWS services have their own namespace, EC2 = AWS/EC2, so you cannot use this for yourself

## Metric
- Collection of related data points
- In a time ordered stucture
	- CPU util
	- Network IO
	- Disk util
- Metric doesn't mean a single server
	- CPU util is a metric
	- It might be coming from many EC2 instances
## Datapoint
- Each measurement sent as a specific metric to the CloudWatch service is a datapoint
- ![[Pasted image 20260425171226.png]]
- How to distinguish between different EC2 instances?

## Dimensions
- Name value pairs
- Allows to separate things, provide different perspectives of things
	- InstanceId, InstanceType
	- ![[Pasted image 20260425171402.png]]

## Alarms
- Linked to a specific metric
- Take action based on a metric based on a configuration
- OK <-> ALARM <-> INSUFFICIENT DATA state