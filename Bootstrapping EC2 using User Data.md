- Bootstrapping allows EC2 Build Automation
	- Bring instance to configured state
- User Data - Accessed via the meta-data IP
- http://169.254.169.254/latest/user-data
- Anything you pass in, instance OS executes
	- ONlLY once, at launch time
	- Restarts don't count
- EC2 doesn't interpret, the OS needs to understand the user data

- Software in OS that listens for user-data and spawns a root process to execute if any is injected from the EC2 service
- ![[Pasted image 20261015225713.png]]
- It's opaque to EC2, just a block of data
- It's not secure, don't use for passwords or long term credentials
- User data is limited to 16kb in size
	- Or Script to download that data
- Can be modified when instance stopped
- But only executed once at launch

Boot-time-to-service-time
- Metric, how quickly after you launch an instance is it ready for service
- Bootstrapping - reduces post launch time
- AMI bake - front loaded reducing of post launch time
- ![[Pasted image 20261015230349.png]]

`/var/log` - cloud-init.log & cloud-init-output.log