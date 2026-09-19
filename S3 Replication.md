2 Types
- CRR (Cross-Region Replication)
- SRR (Same-Region Replication)

Both support the same or different accounts buckets
- A Replication configuration applied to source bucket
- From source to destination, configuration determines
	- Which destination to use
	- IAM role to use for the replication, permissions to
		- Read Obj on source
		- Replicate Obj on destination
	- Replication encrypted
- For same account, IAM role should have automatic access to both buckets
- For different accounts, IAM role is not trusted by the destination account
	- Add bucket policy on destination bucket (resource policy)

# Replication Options
- All objects OR subset - filter by a rule
- Storage class - default is to maintain
- Ownership - default is the source account, even if through different accounts
- Replication Time Control (RTC), applies 15 mins SLA of replication time

# Replication Considerations