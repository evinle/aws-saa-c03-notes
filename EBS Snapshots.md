- Backup to S3, protects against AZ issues
- Migrate AZ-bound data to other AZs or region

- Snapshots are incremental volume copies to S3
- First snapshot = full copy of 'data'
- Future snapshots = incremental
- Volumes can be created (restored) from snapshots
- ![[Pasted image 20261003213758.png]]

## Performance
- New EBS Volume = full performance immediately
- Snaps restore lazily - fetched gradually
- Requested blocks are fetched immediately
- Force a read of all data immediately to guarantee perfect performance
- Fast Snapshot Restore (FSR) - Immediate restore
	- Up to 50 snaps per region. 
	- Set on Snap & AZ - combination to account for 1 fast snap restore set

## Consumption and Billing
- Billed by Gigabyte-month
- 10 GB stored for 1 month = 10 GB month
- 20 GB stored for 1/2 month = 10 GB month
- For used data, not allocated data
- ![[Pasted image 20261003214441.png]]