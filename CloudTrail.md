- Logs things that happens in an AWS account
	- Creating Bucket
	- Stopping EC2 instance
	- Add SG

- Logged API Calls/Events are CloudTrail Events
	- Management Events
	- Data Events
	- Insight Events
- Last 90 days storage
	- No Cost
	- Enabled by Default
- To Customise, you need to create a Trail

## Management Events
- Control Plane Operations
	- Create EC2, Terminating EC2, Creating VPC

## Data Events
- Resource Operations
	- Objects uploaded to S3, accessed from S3, Lambda Invoked
- By default not logged

## Trail
- Unit of Configuration
- Logs Events for the AWS Region it's created in
- One Region Trail vs All Regions Trail
	- All Regions Trail is a collection of Trail, grouped logically
- Regional Services vs Global Services
	- Regional Services generally log to their respective region
	- Global Services log to us-east-1
	- Global Services: IAM, STS, CloudFront
- When Trail configured, can store in S3 bucket under compressed JSON, or import into cloudwatch logs
	- By default, if no trail configured, data not stored in s3, only retained for 90 days
- NOT REALTIME - maybe after 15 mins

![[Pasted image 20260816150124.png]]

## Pricing
- 90 days retention - default, free
- One copy of Management Events, in S3, in each region, for each account
- Everything above that for Management Events, you'd have to pay
- You have to pay by default for any other types of events
- S3 only has costs associated, both with requests + storage