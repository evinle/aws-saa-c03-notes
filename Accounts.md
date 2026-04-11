## Overview 
- Think of it as a container that holds
	- Identities 
	- Resources
- Has a unique email address and payment
- Always has a root user 
	- Has full control
	- Can't be restricted
- Contains payment method, which will be billed on usage
- IAM - Identity Access Management
	- Can be Users, Groups or Roles
	- Can be granted or revoked access to any or all resources WITHIN the account
	- Starts of with no permissions
-  AWS Accounts can contain the impact of admin errors, or exploits by bad actors. Use seperate accounts for seperate things (DEV, TEST, PROD) or teams or products or clients
- ![[Pasted image 20260411102035.png]]

## MFA - Multi Factor Authentication
- Factors - different pieces of evidence which prove identity
	- Knowledge
		- Password
	- Possession
		- Bank card, etc.
	- Inherent
		- Fingerprint, face, voice, etc.
	- Location
		- Physical location 
		- Network location
- Encodes the secret + account id (like JWT?)
![[Pasted image 20260411103233.png]]

