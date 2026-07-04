Large business - multiple AWS accounts

- Standard AWS Account
- Not within an organisation
- Using the account to create the org - management account "Master"
- Invite existing accounts to join the org - "Member" accounts
- Create new accounts within an org - just need a valid unique email

- Structure of accounts within an org
- Inverted tree, hierarchical
- Organization Root - container within org 
	- Contain accounts 
	- Other containers - Organizational Unit (OU)
	![[Pasted image 20260628173409.png]]
- Member accounts pass their billing through to Management Account
	- "Payer" account

- Certain services you can pay in advance in exchange for cheaper rates
- Org benefits from the whole pool of reservations and volume used

### Best practice for access control
- IAM roles used to grant users permissions
- Single AWS Account that contains all the identities that are logged into
- Other identities' identity federation
- Role Switch from the account to other member accounts
- ![[Pasted image 20260628174331.png]]


## Thoughts
- A role is a connector - a relationship type, connecting certain accounts/identities/groups to a set of permissions
- They can be assumed temporarily to complete a certain task
- They're the building block for higher level services like IAM Identity Centre, which allows federation of identity through letting the service assume the role on behalf of the user
- 