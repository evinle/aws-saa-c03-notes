# Review 2026-10-18-0837-quick

## Missed concepts
- **scp-restricts-member-root** (Q02): you picked C (an allow-list SCP with only CloudTrail reads). That would remove every other permission in all 40 accounts. An explicit-deny SCP on the organization root blocks just the two actions, root users included. Re-read [[Service Control Policy]]: "Explicit Deny always wins"; "Allow list: more restrictive, easier to mistakenly deny something".
- **ec2-autorecovery-system-check** (Q04): you picked C (an Auto Scaling group with min/max/desired of 1). The ASG launches a *new* instance, so the instance ID and private IP change. A CloudWatch alarm on the **system** status check with the recover action keeps the same instance and moves it to new hardware in the same AZ. Re-read [[EC2 Instance Status Checks and Autorecovery]].
- **instance-store-beyond-ebs-iops** (Q07): you picked B (io2 Block Express). It maxes out at about 256,000 IOPS per volume, and EBS is capped at about 260,000 per instance. Above that, only instance store works, and losing a node's data is acceptable when the application replicates itself. Re-read [[Choosing between EC2 Instance Store and EBS]]: "More than 260000 IOPS - instance store".

## Notes to revisit
- [[Service Control Policy]]
- [[EC2 Instance Status Checks and Autorecovery]]
- [[Choosing between EC2 Instance Store and EBS]]

## Gaps: no note for X
- (none in this run; every question was grounded in a note)

## Note issues
Logged in [[Quizzes/NOTE-ISSUES]] while this quiz was being written:
- [[Key Management Service (KMS)]]: customer managed key rotation is disabled by default, not enabled
- [[EC2 Purchase Options (Launch Types)]]: "No Upfront" is listed twice; the last should be All Upfront
- [[EC2 Reserve Instances]]: Scheduled RIs are no longer offered
