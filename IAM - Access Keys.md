- A type of Long Term Credential 
	- Long Term Credentials are always used with users
- Don't change regularly/update

# IAM User
- Can only have a maximum of 1 username and 1 password - password could even be optional
- Can have 0 - 2 access keys

## Access Keys
- 2 Parts
	- Access Key ID
	- Secret Access Key
- Cannot change, if leaked, will have to be deleted and generate a new one
- Typical workflow is 
	- Generate new access key
	- Update all clis and apps to use new access key
	- Delete the old one
- IAM users are the only identity that uses access keys
	- Except for root (not recommended!)

- Can be created in the Security Credentials page in AWS
- Download the CSV

## Configuring Profile
`aws configure --profile iamadmin-general`
- Prompted for
	- Key ID
	- Secret Key
	- default region (why is this us-east-1)
		- Because it was the first
		- IAM, Route53, CloudFront, technically anchored
		- Gets newest features first
		- Pricing
		- Dense internet access point
		- Default copy paste region
		
`aws s3 ls --profile iamadmin-general`
