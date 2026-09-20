- Group of features, enabled on 'new' buckets
 - Requires versioning
 - Once turned on, can't disable, and versioning cannot be suspended
 - WORM (Write Once Read Many) - No Delete, No Overwrite
 - Individual versions are locked
 - 2 ways that object retention is managed
	 - Retention period
	 - Legal Hold
	 - Can have both, one or the other, or none
	 - Defined on individual object versions or set a bucket default

# S3 Object Lock - Retention
- Retention Period - In Days & Years
- 2 Modes
	- Compliance - can't be adjusted, deleted, overwritten
		- Retention period cannot be adjusted
		- Retention mode cannot be adjusted 
		- Strictest
	- Governance
		- Special permission can be granted to allow lock settings to be adjusted
		- "s3:BypassGovernanceRetention"
		- z-amz-bypass-governance-retention:true (console default)

# S3 Object Lock - Legal Hold
- ON or OFF - no retention
- No Deletes or Changes until removed
- s3:putObjectLegalHold is required to add or remove
- Prevent accidental deletion
- ![[Pasted image 20260920150224.png]]
