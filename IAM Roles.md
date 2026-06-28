- Short term
- Represents a level of access that you borrow
- Could be used when you can't pin point the exact amount of users, when you need to give access to external principals, identity or systems, or when > 5000 IAM users
![[Pasted image 20260628135009.png]]

## Policy Types
- Trust Policy
	- Who's allowed to assume the role
	- Can reference identities in the same account
		- Other IAM users, roles, aws services
	- Other AWS accounts
	- Temporary Security Credentials = timed-limited access keys
	- ![[Pasted image 20260628135738.png]]
- Permissions Policy
	- What can be done with the temp credentials
- Roles can be referenced within Resource Policies - s3-attached access permissions
- `sts:AssumeRole`


## When to use
- At lambda invocation time, runtime assumes the role to get access to other AWS services
- Unknown number of principals
- ![[Pasted image 20260628140325.png]]


![[Pasted image 20260628141030.png]]


![[Pasted image 20260628141245.png]]
- External IDs cannot be used directly to access AWS Resources

