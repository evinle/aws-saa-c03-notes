![[Pasted image 20260922214825.png]]
- Inbound vs Outbound requests is a matter of perspective

# Stateless firewalls
- Even if the request that comes in and response that comes out is part of one client-server interaction, there needs to be 2 firewall rules for the inbound and the outbound
- This is exacerbated if the server itself needs to reach out to somewhere (e.g. software updates), so now it's playing the role of the client
- 
![[Pasted image 20260922215440.png]]

- Request needs to be to a well known port

# Stateful firewalls
- Intelligent enough to identify a request and a response
- ![[Pasted image 20260922220218.png]]

