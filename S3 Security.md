- S3 is private by default
- Root user of the account that owns the bucket is the only one with access

## S3 Bucket Policy
- A form of resource policy
- Like identity policies, but attached to a resource (bucket)
- Perspective of resources
	- Identity Policies can only control identities in your own accounts
- Resource Policies can allow/deny from different accounts, including Anonymous principals
![[Pasted image 20260823164326.png]]
- Good way to grant anonymous access

![[Pasted image 20260823164522.png]]
- Denies anyone who doesn't have the "1.3.3.7/32" IP address, whitelisting

![[Pasted image 20260823164643.png]]
- Denies anyone who doesn't have MFA to boris
- Allow rest

- Access is always Identity Policy + Resource Policy (unless anonymous)

## Access Control Lists (ACL)
- Is a subresource
- Legacy
- Inflexible, Simply Permissions
- Best to ignore

## Block Public Access
- Only blocks anonymous principal
- Sits on top of bucket policies
- Because of PR disasters

## Exam Powerup
- Which one to use, Identity vs Bucket policy
- Often personal choice
![[Pasted image 20260823165427.png]]