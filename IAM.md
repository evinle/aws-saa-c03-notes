## Overview
- Root User is fully trusted by the account
- Could be thought of as 1
- LPA - Least Privileged Access
	- Give only the least privileges to get a job done
- If root is compromised, access cannot be restricted
![[Pasted image 20260411105305.png]]
- Every AWS Account 
	- Has its own copy of IAM - it's own DB
	- Globally resilient service - any data is always secure across all AWS regions
	- Your own dedicated instance - separate from all other accounts

## Identities
3 main types: Users, Groups and Roles
![[Pasted image 20260411105814.png]]
### Users
- Single User/Application
- Used when you can identify the single user
### Groups
- Grant an uncertain amount of users 
### Roles
- Gives services (i.e. EC2) permissions to access other services (i.e. S3)
- Gives external accounts access to other services
- Used when number of things is uncertain

### Policy
- Used to allow or deny access to certain services
- Only when they're attached to identities (User, Group, Role)

## What's its job?
- IDP - Identity provider
- Authenticate
	- Prove your identity - who you say you are
	- When they try to connect, they're known as a Security Principal
- Authorize
	- Allow or Deny access to certain resources
## Cost
- No Cost, though there are limits
- Global Service - Globally resilient
- Only manage the services and accounts within itself
- Identity Federation - use existing identities to access 

