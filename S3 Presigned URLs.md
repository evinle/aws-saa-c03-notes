- ![[Pasted image 20260920131512.png]]
- Solves the problem of giving temporary access to unauthenticated identities
- Will use the url's creator's identity + permissions
- ![[Pasted image 20260920131848.png]]

# Exam PowerUp
- You can create a presigned URL for an object you have no access to
- Matches the the permissions of identity that generated the URL at that moment - the identity could have lost access
- Don't generate with a role.. URL stops working when temporary credentials expire