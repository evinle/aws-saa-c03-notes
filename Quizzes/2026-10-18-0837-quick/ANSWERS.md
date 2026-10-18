# Answers 2026-10-18-0837-quick

## Key

| Q | Answer | Type | Domain | Task | Notes | Concept tag | Beyond notes | Origin |
|---|---|---|---|---|---|---|---|---|
| Q01 | C | MC | 1 Secure | 1.3 | [[S3 Object Encryption - CSE SSE]], [[Key Management Service (KMS)]] | sse-kms-role-separation | no | new |
| Q02 | B | MC | 1 Secure | 1.1 | [[Service Control Policy]], [[AWS Organizations]] | scp-restricts-member-root | no | new |
| Q03 | B, D | MR2 | 1 Secure | 1.2 | [[Network Access Control List (NACL)]], [[Security Groups (SG)]] | nacl-deny-order-sg-reference | no | new |
| Q04 | A | MC | 2 Resilient | 2.2 | [[EC2 Instance Status Checks and Autorecovery]] | ec2-autorecovery-system-check | no | new |
| Q05 | C | MC | 2 Resilient | 2.2 | [[S3 Replication]] | s3-replication-not-retroactive | no | new |
| Q06 | D | MC | 2 Resilient | 2.2 | [[S3 Replication]], [[IAM Roles]] | s3-crr-cross-account-bucket-policy | no | new |
| Q07 | A | MC | 3 High-Performing | 3.1 | [[Choosing between EC2 Instance Store and EBS]], [[Instance Store Volumes]], [[EBS Volume Type - Provisioned IOPS]] | instance-store-beyond-ebs-iops | no | new |
| Q08 | A, C | MR2 | 3 High-Performing | 3.1 | [[S3 Performance Optimization]] | s3-multipart-transfer-acceleration | no | new |
| Q09 | B | MC | 4 Cost-Optimized | 4.1 | [[S3 Object Storage Classes]], [[S3 Lifecycle configuration]] | s3-glacier-flexible-retrieval-time | no | new |
| Q10 | D | MC | 4 Cost-Optimized | 4.2 | [[EC2 Reserve Instances]], [[EC2 Purchase Options (Launch Types)]] | compute-savings-plan-flexibility | no | new |

Grading: all-or-nothing. A question is correct only if the ticked set equals the answer set exactly.

## Explanations

### Q01: C
**Deciding keyword:** "S3 administrators ... cannot read the report contents" plus "LEAST operational overhead"
**Why C:** SSE-KMS gives role separation. S3 permissions alone can't decrypt; the caller also needs kms:Decrypt from the key policy. A customer managed key lets the security team own the key and its rotation.
**Why not A:** SSE-S3 gives no control over the key or its rotation, and anyone with S3 read access can read the objects.
**Why not B:** SSE-C meets the control requirements, but the team must generate, rotate, store and send the key with every request. That's far more overhead.
**Why not D:** Client-side encryption works but makes the application handle encryption and key management. That's the most overhead of all the options.
**Review:** [[S3 Object Encryption - CSE SSE]] → SSE-S3 "Can't stop s3 admin from decryption"; SSE-KMS "Enables role separation". [[Key Management Service (KMS)]] → customer managed keys are "more configurable".

### Q02: B
**Deciding keyword:** "including each account's root user" plus "preventive"
**Why B:** SCPs set the maximum permissions for every identity in a member account, root user included, and an explicit deny always wins. Attaching the SCP to the organization root covers all 40 accounts and any added later.
**Why not A:** IAM policies can't restrict the root user, and keeping them in 40 accounts is ongoing work.
**Why not C:** An allow list that contains only CloudTrail reads would remove every other permission in every account.
**Why not D:** AWS Config remediation is detective. It reacts after logging has already stopped.
**Review:** [[Service Control Policy]] → "Limits what an account can do, including the `root` user"; "Explicit Deny always wins". (SCPs never restrict the management account itself.)

### Q03: B, D
**Deciding keyword:** "block" (needs an explicit deny) plus "even as web instances are launched and terminated"
**Why B:** NACLs support explicit deny, and rules are evaluated from the lowest number, stopping at the first match. Rule 50 is checked before the allow at rule 100.
**Why D:** A security group can reference another security group, so any instance carrying the web SG is allowed automatically as the group scales.
**Why not A:** Security groups have no explicit deny, only allow rules plus an implicit deny.
**Why not C:** Rule 200 is never reached for HTTPS traffic because rule 100 already matched and allowed it.
**Why not E:** Fixed IP addresses go stale as the Auto Scaling group replaces instances.
**Review:** [[Network Access Control List (NACL)]] → "Starts from lowest rule number, the stops when matched"; "Use together with SG to add explicit DENY". [[Security Groups (SG)]] → "No explicit DENY"; "SG Logical References".

### Q04: A
**Deciding keyword:** "underlying host hardware fails" plus "same instance ID, private IP address"
**Why A:** Host hardware failure shows up in the system status check. A CloudWatch alarm on that check with the recover action moves the instance to new hardware in the same AZ. The instance ID, private IP and EBS volumes stay the same.
**Why not B:** The instance status check covers in-guest problems (corrupted file system, kernel, OS networking). Moving to a new host doesn't fix those, and the recover action is tied to the system check.
**Why not C:** An Auto Scaling group replaces the instance with a new one, so the instance ID and private IP change.
**Why not D:** Termination protection prevents accidental termination. It does nothing when hardware fails.
**Review:** [[EC2 Instance Status Checks and Autorecovery]] → "System status failure: Power, network, host software/hardware"; "Create Status check alarm ... Recover"; "Can only recover into same AZ".

### Q05: C
**Deciding keyword:** "none of the existing records"
**Why C:** Replication isn't retroactive. Only objects written after the rule is created are replicated. S3 Batch Replication is the built-in way to copy existing objects.
**Why not A:** RTC adds a 15-minute replication SLA for new objects. It doesn't backfill old ones.
**Why not B:** Recreating the rule still only replicates new writes.
**Why not D:** Lifecycle actions are not replicated, and transitions don't produce new writes that would be replicated.
**Review:** [[S3 Replication]] → "By Default, not retroactive ... Batch replication can replicate existing objs"; "No system events (lifecycle)".

### Q06: D
**Deciding keyword:** "separate backup account" plus "Access Denied", with the role's own permissions already correct
**Why D:** Across accounts, the destination account doesn't trust the source account's role. The destination bucket needs a bucket policy (resource policy) that allows the role to replicate into it.
**Why not A:** The role already has the right identity permissions. Cross-account access needs the resource side to allow it too.
**Why not B:** Changing object ownership doesn't grant access. It needs the destination permissions as well.
**Why not C:** Replication uses an IAM role, not stored access keys, and long-term keys are worse security practice.
**Review:** [[S3 Replication]] → "For different accounts, IAM role is not trusted by the destination account; Add bucket policy on destination bucket".

### Q07: A
**Deciding keyword:** "more than 300,000 random IOPS" plus the database replicating and rebuilding nodes itself
**Why A:** Instance store is the highest-performing storage in AWS and goes beyond what EBS can reach on one instance. Its data loss on a stop or host change is acceptable because the database replicates across nodes and rebuilds failed ones.
**Why not B:** io2 Block Express tops out around 256,000 IOPS per volume, below the requirement.
**Why not C:** RAID 0 across EBS volumes is still capped by the per-instance EBS limit of about 260,000 IOPS.
**Why not D:** EFS is network file storage with higher latency and isn't built for per-node block IOPS at this level.
**Review:** [[Choosing between EC2 Instance Store and EBS]] → "More than 260000 IOPS - instance store"; "Resilience w/ App in-built replication -> it depends". [[EBS Volume Type - Provisioned IOPS]] → Block Express "Up to 256000 IOPS".

### Q08: A, C
**Deciding keyword:** "Australia and Europe" to us-east-1 (distance), and "whole upload to start again" (single stream)
**Why A:** Transfer Acceleration sends uploads into the nearest edge location and then over the AWS network rather than the public internet. The bucket name has no periods and is DNS-compatible, so it qualifies.
**Why C:** Multipart upload sends parts in parallel, and a failed part is retried on its own, so the whole upload doesn't restart.
**Why not B:** Presigned URLs grant access. They don't change speed or resilience.
**Why not D:** Key prefixes spread request rate across partitions. They don't help the throughput of a single large upload.
**Why not E:** Storage class affects cost and durability, not upload speed.
**Review:** [[S3 Performance Optimization]] → single stream "Requires full restart"; multipart "Parts can fail and be restarted in isolation"; Transfer Acceleration "Name cannot contain periods".

### Q09: B
**Deciding keyword:** "MOST cost-effective" plus "retrieval time of up to 5 hours"
**Why B:** Glacier Flexible Retrieval is much cheaper to store than the IA classes, and its Standard retrieval (3–5 hours) fits the audit window. A 1 GB archive makes the per-object overhead negligible.
**Why not A:** Standard-IA works, but it costs far more to store for 11 months of rarely accessed data.
**Why not C:** Deep Archive's Standard retrieval takes about 12 hours, which misses the 5-hour requirement.
**Why not D:** The access pattern is known in advance, so Intelligent-Tiering's monitoring fee buys nothing. Its automatic tiers also wouldn't reach archive tiers this cheaply without opt-in.
**Review:** [[S3 Object Storage Classes]] → Glacier Flexible "Standard: 3-5 hours"; Deep Archive "Standard: 12 hours"; Intelligent-Tiering "Monitoring and automation cost". [[S3 Lifecycle configuration]].

### Q10: D
**Deciding keyword:** "move ... to AWS Fargate and AWS Lambda" plus "change instance families"
**Why D:** A Compute Savings Plan is an hourly spend commitment that applies across EC2 (any family, size or Region), Fargate and Lambda.
**Why not A:** Standard RIs are locked to an instance type and don't cover Fargate or Lambda.
**Why not B:** Spot can be interrupted, which doesn't suit a steady 24/7 baseline.
**Why not C:** An EC2 Instance Savings Plan allows changes of size and OS within one instance family, but not changes of family or moves to Fargate and Lambda.
**Review:** [[EC2 Reserve Instances]] → "General compute ... EC2, Fargate & Lambda"; "EC2 Savings plan - flexibility on size & OS".
