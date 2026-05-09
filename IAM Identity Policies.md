![[IAM#Identities]]

Policies attached to Identities

## IAM Policy Document

- Authenticate Identity
- Made up of statements
### Statements
1. Sid - Statement Id - optional - describes 
2. Resource + Action
	- How the policy is matched
	- When an Authenticated user is performing a certain Action on a specific resource
	- Can have wildcards
	- Actions has `type:action` i.e. `s3:*`
	- Resource has `*` or arn
- Effect will apply when matched against resource and action - `Allow` or `Deny`

![[Pasted image 20260509140038.png]]

## Overlapping Allows and Denys
- Can have overlapping effects 
- ![[Pasted image 20260509140835.png]]
- By Default, all access denied
- Explicit ALLOW goes on top
- Explicit DENY always win

## Types of Policy
- Inline - individual policies, not connected, applied to specific identities, exceptional
- Managed - own object, reusable, low management overhead
	- AWS Managed
	- Customer Managed
	![[Pasted image 20260509141430.png]]

## IAM Users
- Identity used for...
- Anything requiring long-term AWS access
- Humans, Apps, Service Accounts, etc.
- Usually if you can picture 1 named thing, correct identity is an IAM User

Principle
- Entity trying to access 
- Needs to be authenticated and authorized to interact with a resource
- Can authenticate through Username & Password OR Access keys
- If successful, becomes Authenticated Identity
	- Proven to AWS it is the identity that it claims to be
- Authorization checks if the Authenticated Identity does have access by looking at policies
- ![[Pasted image 20260509142659.png]]

## Amazon Resource Names
- Uniquely identify resources within any AWS accounts
- ![[Pasted image 20260509143304.png]]

## Exam Powerup
- 5000 IAM Users per account
- IAM User can be a member of 10 groups
- 