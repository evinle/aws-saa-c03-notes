# Create Database Instance
- First need to create a DB subnet group
	- Basically group subnet groups from different AZs for use with our DB

- Then create an instance and assign new security group
``` bash
# Create security group
aws ec2 create-security-group --group-name SG-NAME --description DESCRIPTION --vpc-id VPC-ID

# Create RDS instance
aws rds create-db-instance --db-instance-identifier IDENTIFIER --db-instance-class CLASS --engine postgres --master-username USERNAME --master-user-password PASSWORD --allocated-storage STORAGE --vpc-security-group-ids SG-ID --no-publicly-accessible --backup-retention-period DAYS
```

# Configure Security Groups
- Need inbound (ingress) rule to allow web server from our public subnet to be able to reach our db in subnet 
	- Done by assigning rule to the public security group
- Need outbound (egress) rule from web server to allow it to talk to the db from its sg
	- Done by assigning a rule to 
```bash
# Add outbound rule to app server security group (assuming you want a specific rule)
aws ec2 authorize-security-group-egress --group-id APP-SG-ID --ip-permissions IpProtocol=tcp,FromPort=5432,ToPort=5432,UserIdGroupPairs=[{GroupId=RDS-SG-ID}]

# Add inbound rule to DB security group
aws ec2 authorize-security-group-ingress --group-id RDS-SG-ID --ip-permissions IpProtocol=tcp,FromPort=5432,ToPort=5432,UserIdGroupPairs=[{GroupId=APP-SG-ID}]
```

# On IOPS
- gp3 - all purpose storage ~ 3000 - 16000 IOPS (scalable) + cost effective
- io1/io2 - provisioned IOPS - 1000 - 256000 IOPS - large databases
> There's also the older gp2 which scales IOPS per GB. It can be cheaper, but it has an I/O operations cost associated with it. The rule of thumb is to use gp3 until you hit a bottleneck.

# Backups
- Stored in S3
> Cost check: Backups cost money. A 7-day retention period means you're storing 7 days of backups (at ~$0.095/GB/month). For a 20 GB database that can be ~140 GB of backup storage. Monitor backup costs, and reduce retention or delete snapshots when done
- RDS backups include:
	- Full database snapshot: Complete copy of your database at a point in time
	- Transaction logs: All changes since the last backup (enables point-in-time recovery)

## Backup Modes
- Full restore 
	- Up to the second disaster struck
	- Uses full backup + transaction logs
	
- Restore from Snapshot
	- Restore to a known good state
	- Can create snapshot at anytime
	- Faster
	
- Restore to new Instance
	- All restores create a new database instance
	- Original instance remains unchanged
	- This means "restoring" is also useful for testing, cloning, or migration

# Read Replica
```bash
aws rds create-db-instance-read-replica --db-instance-identifier patientping-replica --source-db-instance-identifier patientping-db --db-instance-class db.t3.micro --vpc-security-group-ids YOUR-SG-ID --db-subnet-group-name patientping-private-subnet-group --no-publicly-accessible
``` 

#