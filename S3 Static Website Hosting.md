- Normal Access via AWS API
- Enable hosting
	- Set up Index and Error document
- AWS creates a website endpoint - automatic
	- can use custom domain with Route53 - bucketname must match domain
	- good idea to reserve the name at bucket creation time

![[Pasted image 20260823170426.png]]

## Pricing
- Store data /GB/month
- Data transfer fee - out - in is free, out is paid
- Requesting data - every GET, POST, PUT, LIST, COPY - per 1000 operations
