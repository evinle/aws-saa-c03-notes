## Server Side Encryption
- Buckets aren't encrypted, objects are
- ![[Pasted image 20260906212113.png]]

- SSE-C - Serverside with Customer Provided Key
- SSE-S3 - with S3 Managed Keys
- SSE-KMS - with KMS Keys

## SSE-C
- AWS does encryption/decryption
- ![[Pasted image 20260906212647.png]]

## SSE-S3
- both encryption/decryption & keys
- ![[Pasted image 20260906212819.png]]
- Can't control key
- Can't control rotation
- Can't stop s3 admin from decryption

## SSE-KMS
- Using DEK
- Enables role separation
- ![[Pasted image 20260906213502.png]]
## Summary![[Pasted image 20260906213557.png]]