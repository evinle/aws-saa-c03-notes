# S3 Standard
- Replicated across at least 3 AZs
- 11 9s of durability
	- MD5 Checksum 
	- CRC to detect data detection
- HTTP/1.1 200 OK - signal that obj is stored durably 
- Cost
	- GB/month fee for data stored
	- GB transfer out
	- per 1000 requests
- milliseconds first byte latency
- publicly available
# S3 Standard-IA (Infrequent Access)
- Same durability and availability
- First byte latency is the same
- Cost
	- Much cheaper (about 1/2) for storage
	- Same costs for transfer out and 1000 requests
	- Retrieval fee - GB of data retrieved
	- Minimum duration charge of 30 days
	- Min capacity charge of 128kb per object
# S3 One Zone-IA
- Retrieval fee, minimum duration + capacity
- Only stored in one AZ
- Non critical data or replaceable data only

# S3 Glacier - Instant 
- Like S3 Standard-IA but
	- Cheaper storage
	- More expensive retrieval
	- Longer minimum
- Min storage duration - 90 days
- Still instant access

# S3 Glacier - Flexible
- Cold objects - aren't immediately available, can't be made public
	- Just a pointer to that object
	- Need to do retrieval to gain access
- Retrieve, stored S3 Standard-IA temporarily
	- Expedited: 1-5 mins
	- Standard: 3-5 hours
	- Bulk: 5-12 hours
	- More to less expensive
- First byte latency = minutes or hours
- Archival data - frequent or realtime access is not needed

# S3 Glacier Deep Archive
- 40KB min size
- 180 Day min duration
- No public access, requires retrieval
- Retrieval ranges
	- Standard: 12 hours
	- Bulk: up to 48hours


# S3 Intelligent-Tiering
- 5 different tiers
- Range of ways an object can be stored
- Tiering system moves it between tiers automatically for you
	- Monitors usage of an object
	- Not accessed 30 days - moved to IA
	- 90 days - Archive Instant Access
	- 90-270 days - Archive
	- 180 or 730 days - Deep Archive
	- ![[Pasted image 20260919162023.png]]
- Monitoring and automation cost per 1000 objects