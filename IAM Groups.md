Container for IAM Users
CANNOT Log in to a group

![[Pasted image 20260509162927.png]]
- No limit for no. users in a group
- NO Nesting
- 300 Groups per account

> Policies can also be attached to resources - Resources Policies, can reference identities - IAM Users and IAM Roles by using their ARN, i.e. a bucket can have a policy to allow specific users access
- Groups are not a true identity
- Can't be referenced as a principal in a policy
- Simply a container for IAM users - that's it
