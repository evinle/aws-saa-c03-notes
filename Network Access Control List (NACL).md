- Like a traditionnal firewall
- Every subnet has a NACL
	- Inbound and outbound
	- Connections within the subnet are not affected
- Contains 2 sets of rules
	- Inbound rules 
		- Data entering the subnet
	- Outbound rules
		- Data leaving the subnet
- NACL is stateless - don't know if traffic is request or response
	- Rules match DST IP/IP Range, Port/Port range + protocol
	- Explicit allow + explicit deny
	- Starts from lowest rule number, the stops when matched
	- `*` catch all, implicit deny

![[Pasted image 20260922222100.png]]

# Example

![[Pasted image 20260922222352.png]]

![[Pasted image 20260922222533.png]]

# Default NACL
- By default has a `*` deny, but also a `100` allow, so no effect
![[Pasted image 20260922222646.png]]

# Custom NACL
- By default has only the `*` deny, so denies all
![[Pasted image 20260922222744.png]]

# Misc
- Only filters by IPs/CIDR, ports & protocol - no logical resource
- Cannot be assigned to AWS resources - just subnets
- Use together with SG to add explicit DENY
