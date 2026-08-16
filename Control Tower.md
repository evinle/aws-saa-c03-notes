- Quick and Easy setup for multi-account environment
- Orchestrates other services, sits on top of
	- Organization, IAM Identity Center, CloudFormation, Config, etc.
- Landing Zone - multi account environment
	- SSO/ID Federation, Logging, Auditing
- Guard Rails - rules/standards across all accounts
- Account Factory - Automate & Standardize new account creation
- Dashboard

![[Pasted image 20260816160257.png]]


## Landing Zone
- Home Region
	- Region you initially deploy the product into
	- Can allow or deny the usage of other regions
- Built with Org, Config, CloudFormation
- Foundational OU = Security - Log Archive & Audit Accounts
- Custom OU = Sandboxed - Test
- IAM Identity Center (a.k.a AWS SSO) - SSO, multi accounts, ID Federation
- Monitoring & Notifications - CloudWatch + SNS
- End user account provisioning via Service Catalog

## Guard Rails
- Are rules
- Mandatory, Strongly Recommended, Elective
- Preventative - Stop you from doing something (SCP) - enforced or not enabled
- Detective - compliance check - (CONFIG rules) - clear, in violation or not enabled

## Account Factory
- Automated Account Privisioning
	- Can be done by cloud admins or end users with enough permissions
- Guardrails - can be automatically added
- Account admin given to a named user (IAM Identity Center)
- Account & network standard configuration
- Allow any members of your org to be able to provision accounts for any purpose which you allow
- Accounts can be closed or repurposed
- Can be integrated with APIs - according to SDLC (Software Development Lifecycle)

