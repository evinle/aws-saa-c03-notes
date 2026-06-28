- Short term
- Represents a level of access that you borrow
- Could be used when you can't pin point the exact amount of users, when you need to give access to external principals, identity or systems, or when > 5000 IAM users
![[Pasted image 20260628135009.png]]

## Policy Types
- Trust Policy
	- Who's allowed to assume the role
	- Can reference identities in the same account
		- Other IAM users, roles, aws services
	- Other AWS accounts
	- Temporary Security Credentials = timed-limited access keys
	- ![[Pasted image 20260628135738.png]]
- Permissions Policy
	- What can be done with the temp credentials
- Roles can be referenced within Resource Policies - s3-attached access permissions
- `sts:AssumeRole`


## When to use
### Lambda Invocation
- ![[Pasted image 20260628140325.png]]
- At lambda invocation time, runtime assumes the role to get access to other AWS services
- Unknown number of principals

### Break glass 
![[Pasted image 20260628141030.png]]
- Help desk only need read only, to prevent them from doing desctructive things they're not experienced enough to do
- Sometimes in an emergency, assuming the role to restart an EC2 or something is necessary - break glass - will be logged, only available for a short time, and only in cases where it's genuinely needed

### Federated Identity
![[Pasted image 20260628141245.png]]
- External IDs cannot be used directly to access AWS Resources
- If more than 5000 people, don't need to manage 5000+ extra accounts 

Web Identity Federation
![[Pasted image 20260628141742.png]]
- A bit contrived, used when no backend

### Partner Accounts
![[Pasted image 20260628143440.png]]
- Users from your org can assume a role in another partner org (who's the object owner), to make modifications
- 

## GitHub Actions → AWS (OIDC Federation)

**Flow**
- Job starts → GitHub issues a signed JWT (contains `iss`, `aud`, `sub` claims)
- Runner calls `sts:AssumeRoleWithWebIdentity` with the JWT
- STS validates the JWT and issues temporary credentials (no stored secrets)
- Runner uses those credentials to access AWS resources (ECR, ECS, S3, etc.)

**IAM Trust Policy — key fields**
- `Principal.Federated` — the GitHub OIDC provider ARN (external identity, not an AWS one)
- `aud` — audience; who the token is for (`sts.amazonaws.com`)
- `sub` — subject; what triggered the workflow (`repo:org/repo:ref:refs/heads/main`)
  - Lock to a branch, tag, or GitHub environment for least privilege
  - e.g. `repo:my-org/my-repo:environment:production` for prod-only access

```json
{
  "Principal": {
    "Federated": "arn:aws:iam::123456789012:oidc-provider/token.actions.githubusercontent.com"
  },
  "Action": "sts:AssumeRoleWithWebIdentity",
  "Condition": {
    "StringEquals": {
      "token.actions.githubusercontent.com:aud": "sts.amazonaws.com",
      "token.actions.githubusercontent.com:sub": "repo:my-org/my-repo:ref:refs/heads/main"
    }
  }
}
```

**GitHub Actions workflow**

```yaml
jobs:
  deploy:
    permissions:
      id-token: write   # allows runner to request OIDC token
      contents: read
    steps:
      - uses: actions/checkout@v3
      - uses: aws-actions/configure-aws-credentials@v2
        with:
          role-to-assume: arn:aws:iam::123456789012:role/github-deploy-role
          aws-region: ap-southeast-2
      # runner now has temporary AWS credentials
```

**Why OIDC over stored access keys**
- No long-lived credentials to leak or rotate
- Temporary credentials auto-expire
- Audit trail shows exactly which repo/branch triggered AWS actions