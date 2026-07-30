- Can be attached to root Org Container, OU (Organisation Unit), or individual account
- Crucially, cannot be used to restrict "Management Account"
- Limits what an account can do, including the `root` user of the account
![[Pasted image 20260730184731.png]]

- They don't grant permissions
- They define _boundaries_
	- You'd still need to explicitly give permission, SCPs limit the permissions that can be given

## Allow list vs Deny list
- Deny list - by default
### Deny list
- Implicitly Denies by default
	- Hence the default `FullAWSAccess` by default - no op
- Explicit Deny always wins
![[Pasted image 20260730185455.png]]

### Allow list
- More restrictive
- More Admin overhead
- Easier to mistakenly deny something
- ![[Pasted image 20260730185610.png]]

### With Identity Policies
![[Pasted image 20260730185829.png]]

See [[IAM Identity Policies]]

