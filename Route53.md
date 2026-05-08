- Register Domains
- Host zones
- Globally Resilient


## Register Domains
- Has relationships with all the major TLD registries
	- .com, .net, .io, .org
- ![[Pasted image 20260425235645.png]]
- TLD adds NS server records

## Hosted Zones
- DNS as a service
- Create and manage zone files
- Hosted on 4 managed name servers
- Could be public or private (linked to VPC)
- Hosts DNS records

## DNS Records Type
### Nameserver
![[Pasted image 20260426001216.png]]

### A and AAAA
![[Pasted image 20260426001324.png]]

### CNAME
![[Pasted image 20260426001422.png]]

### MX
mail host
![[Pasted image 20260426001731.png]]

### TXT
text record
proving domain ownership
could fight spam - which entities are authorised to send emails on your behalf
![[Pasted image 20260426001930.png]]

## TTL - Time To Live
- How long records should be cached for 
- In seconds
- Non Authoritative when using cached values
- ![[Pasted image 20260426002300.png]]
- 
