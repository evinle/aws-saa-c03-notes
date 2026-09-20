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
- By Default, not retroactive, start replication for objs after it's turned on, not pre-existing objects, versioning needs to be enabled
	- Batch replication can replicate existing objs
- By Default, one way, but bi-directional replication is possible
- Most encryptions work, SSE-KMS needs extra config
- Source bucket owner needs permissions to objects
	- If bucket is shared cross accounts, some objects might not be owned by the bucket owner
- No system events (lifecycle), glacier or glacier deep archive
- By Default, no delete (with delete marker) - can be enabled

# Why use?
- SSR - log aggregation, prod and test sync, resilience with strict sovereignty
- CRR - Global Resilience, latency