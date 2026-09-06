## Object Versioning
- Controlled at bucket level
- Once enabled, can never be disabled
- Can suspend though
- ![[Pasted image 20260906200007.png]]
- Through `id` property (null when versioning disabled)
	- `id` allocated to the new version
	- Current Version = Latest Version
	- If `id` specified, Current Version is returned 
	- ![[Pasted image 20260906200311.png]]
	- Delete marker added if no version specified on delete
	- ![[Pasted image 20260906200500.png]]
	- Space is consumed by all versions

## MFA Delete
- Enabled in versioning configuration
- MFA is required to change bucket versioning state (enabled -> suspended)
- MFA is required to delete versions
- Serial number (MFA) + Code passed with API calls