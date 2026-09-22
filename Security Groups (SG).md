- Stateful - detect response traffic automatically
- Allowed IN or OUT request means the response is automatically allowed
- No explicit DENY, only implicit DENY
	- Can't block specific bad actors
- Supports IP/CIDR and logical resources
	- Including other SGs and itself
- Attached to ENI's (network interface) - not instances/subnets

![[Pasted image 20260922223700.png]]

# SG Logical References
- ![[Pasted image 20260922224023.png]]
- A SG can reference another SG, which means allowing anything with the referenced SG attached to it

## Self Referencing
- Multiple instances of an app that has an SG attached, can allow traffic from its other instances
- ![[Pasted image 20260922224533.png]]