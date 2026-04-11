- Global Storage Platform
	- Regional based - Regional resilient
	- Never leaves unless you explicitly tell it to
	- Have ability to replicate data across AZs and regions
- Public service
	 - Runs from AWS Public Zone
	 - Designed for multi user usage of resources
	 - Movies, Audio, Photos, Text, Large Datasets
	 - Economical
	 - Accessed via UI/CLI/API/HTTP
	 - Default Storage service - unless requirement is not met
- Stores Buckets and Objects in Buckets

## Objects
- Object contains a Key a Value 
- If you know the object key and the bucket it's in
	- You can retrieve the Value
	- A value can range from 0 to 5TB
	- Also contains
		- Version ID
		- Metadata
		- Access Control
		- Subresources
![[Pasted image 20260411152713.png]]

## Buckets
- Buckets are stored in a specific region
- Never leaves unless you explicitly configure
- Blast radius is the region (if a major outtage or data corruption event occurs)
- Bucket name must be GLOBALLY UNIQUE - across all of aws
- Very flat structure 
- Folders are respresented loosely based on the key (/old/Koala1.jpg)
	- Such keys would be represented in the UI as a folder, but it's actually just a name with metadata built in
	- Often referred to as prefixes
![[Pasted image 20260411153252.png]]
- Bucket names restrictions
	- 3 - 63 characters, all lower case, no underscores
	- Must start with a lowercase letter or a number
	- Can't be IP formatted e.g. 1.1.1.1
- 100 soft limit, 1000 hard limit per account
- Unlimited objects, 0 bytes to 5TB

## Patterns
- Object store, not a file or block storage system
	- Accessing the whole of these entities - image, audio
	- Windows Server accessing file system - needs FILE storage system
	- Can't mount as a mount point/drive or volume - needs BLOCK storage
		- Block storage = virtual hard disk
		- EBS = block storage - one thing accessing it at a name
- Great for scale, distribution/upload
- Great for 'offloading' data
- INPUT and OUTPUT to many AWS products