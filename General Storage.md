- Direct (local) attached storage - on the EC2 host, can be lost
- Network attached storage - over the network, highly resilient, EBS
- Ephemeral storage - temp storage
- Persistent storage - permanent - lives past lifetime of the instance

- Block storage - volume presented to the OS as a collection of blocks
	- No in-built structure
	- mountable, bootable
	- OS creates file system on top of it
- File storage - file server, structured, ready made
	- mountable, not bootable
- Object storage - collection of objects
	- not mountable nor bootable

# Storage Performance
- IO (block) size - how big each chunk is
- IOPS - input, output operations per second
- Throughput - amount of data that can be transferred (MB/s)

- Throughput = block size x IOPS
- ![[Pasted image 20261002083403.png]]
