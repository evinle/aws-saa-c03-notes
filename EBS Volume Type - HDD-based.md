# EBS - HDD-based
- st1 - Throughput Optimized
- sc1 - Cold HDD

- Good for sequential reads
- For throughput and economy

## st1 - Throughput optimized
- 125 GB - 16 TB
- Up to 500 IOPS - 1MB block size = Max 500MB/s
- Credit bucket 
	- 40 MB/s/TB base
	- 250 MB/s/TB burst
- Big data, data warehouses, log processing

## sc1 - Cold HDD
- 125 GB - 16 TB
- Up to 250 IOPS - 1MB block size = Max 250MB/s
- Credit bucket
	- 12MB/s/TB base
	- 80MB/s/TB burst
- Lowest cost HDD - less frequently accessed data
- Colder data requiring fewer scans per day

![[Pasted image 20261003210656.png]]