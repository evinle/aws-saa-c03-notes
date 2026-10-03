# General Purpose SSD - GP2
- Volumes 1GB <= storage <= 16TB
- Created with IO credit allocation
- 1 IO credit = 16kb
- IOPS assume 16kb
- 1 IOPS is 1 IO in 1 second
	- 160kb file = 10 IO blocks of 16kb
	- In 1 second = 10 credits / sec = 10 IOPS
- No credit = no IO
- Capacity 5.4 mil IO credits
- Every volume has baseline performance
	- Bucket fills with minimum 100 IO credits / sec, regardless of size
		- Anything above 33.3 GB = 3x size of volume (100GB = 300 IO credits / sec)
- Can burst up to 3000 IOPs by depleting the bucket
- Starts up full (5.4 mil), 30mins @ 3000 IOPS
- If above 1000 GB, baseline is always > 3000 IOPS (burse), no credit system, always achieve baseline
- If above 5.33 TB, 16000 IOPS max
- Great for boot volumes, low-latency interactive apps, dev & test
- Good default
- ![[Pasted image 20261003195809.png]]

# General Purpose SSD - GP3
- 3000 IOPS & 125 MiB/s - standard - regardless of volume size
- 20% cheaper vs GP2
- Extra costs for up to 16000 IOPS or 1000 MiB/s (vs GP2 250 MiB/s)
- Virtual Desktops, medium sized, single instance db (MSSQL, oracle DB), low-latency interactive apps, dev & test, boot volumes
- ![[Pasted image 20261003195821.png]]
