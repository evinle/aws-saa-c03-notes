##  By Default
- Single data stream in s3
	- `s3:PutObject`
- Requires full restart (stream fails - upload fails)
- Speed & reliability = limited to 1 stream
- Any upload up to 5GB

## Multipart Upload
- Data is broken up
- Min size: 100MB
- Limit of 10000, from 5MB to 5GB
	- Last part can be < 5MB
	- Parts can fail and be restarted in isolation
	- Less risk when uploading more data
- Improves transfer rates
- ![[Pasted image 20260906203024.png]]

## S3 Accelerated Transfer (Off)
- Transfer Accelerations
- Uses S3 Edge Locations
- Bucket can be enabled to use it
	- Name cannot contain periods
	- Name must be DNS compatible
	- Enters closest Edge Location instead of Public Internet routes
	- Must use accelerated endpoint to benefit
- Like public transport vs express trains
- ![[Pasted image 20260906203517.png]]

