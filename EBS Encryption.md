- KMS Key, can either be
	- aws/ebs - default kms managed
	- customer managed
- GenerateDataKeyWithoutPlaintext to generate DEK (Data Encryption Key)
- Encrypted DEK is only ever in memory of the EC2 host
- ![[Pasted image 20261004113125.png]]
- Same key can be used when snapshotting to S3 / replicated to another volume
- ![[Pasted image 20261004113301.png]]

# Exam Powerup
- Accounts can be set to 'encrypt by default' - using default KMS Key
- Or choose a KMS Key to use
- KMS Key used to create a per-volume DEK
- Snapshots and future volumes use the same DEK
- Can't change a volume to NOT be encrypted
- OS isn't aware of the encryption, no performance loss, only between host and KMS