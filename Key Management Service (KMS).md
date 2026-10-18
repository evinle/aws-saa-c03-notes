- Used by a lot of other services
- Regional + Public Service
- Create, Store and Manage Keys
- Symmetric + Asymmetric Keys
- Crytographic operations (encrypt, decrypt)
- Keys never leave KMS (FIPS 140-2 Compliance Service (L2))

## KMS Keys
- KMS Keys: also referred to as CMK or Master Keys
	- Logical, container for keys
	- ID, date, policy, desc & state
	- backed by physical key material
	- Generated or imported
	- Can we used to encrypt or decrypt up to 4KB of data
- Not stored on plain text ever on disk
	- May be briefly decrypted in memory
- Keys never leave the KMS product
- ![[Pasted image 20260906205105.png]]

## Data Encryption Keys (DEKs)
- Generated using KMS Key
- GenerateDataKey - works on > 4KB
- It gives you 2 versions: plaintext and ciphertext, one in plaintext, the other encrypted with the physical key
	- You then encrypts the data yourself, then the plaintext key is safe to discard
	- For decryption, you pass the ciphertext key + encrypted data
	- KMS decrypts the ciphertext key with the key that it has, then decrypts the data with the now decrypted ciphertext key
	- ![[Pasted image 20260906205802.png]]
- S3 Generates DEK for every object

## Key Concepts
- Isolated per region, never leaves the region or service
- Encryption and Decryption is done through API
	- Multi-region keys exist, but out of scope for now
- AWS Owned or Customer Owned
	- AWS Owned keys are keys that AWS Services owns and manages
	- For use in multiple accounts, don't need to worry about them
- Custom Owned splits into 2 types
	- AWS Managed - created by S3, as it integrates with KMS, less customizable
	- Customer Managed - more configurable, i.e. cross account access
- Support rotation
	- AWS Managed - can't be disabled, set to rotate once per year
	- Customer Managed - optional, disabled by default (must be enabled), once per year
- Backing Key (and previous backing keys)
	- Old versions can still be decrypted after rotation
- Aliases - per region


## Permissions
- Key Policies (Resource Policy)
	- Every KEY has one
	- Unlike other services, KMS needs to be told keys trust the account they're contained within
- ![[Pasted image 20260906210713.png]]
- 