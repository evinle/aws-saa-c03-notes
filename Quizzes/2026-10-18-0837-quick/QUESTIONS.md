---
mode: quick
topic:
delivery: chat
created: 2026-10-18T08:37
started:
finished:
---

# Quiz 2026-10-18-0837-quick

Tick your answer(s). Multiple-response questions say how many to select.

## Q01

A healthcare company stores patient reports in an Amazon S3 bucket. A new compliance rule requires that objects are encrypted at rest, that the security team controls the encryption key and its rotation, and that S3 administrators who have full S3 permissions cannot read the report contents. The keys may be stored in AWS.

Which solution meets these requirements with the LEAST operational overhead?

- [ ] A. Use server-side encryption with Amazon S3 managed keys (SSE-S3) as the bucket's default encryption.
- [ ] B. Use server-side encryption with customer-provided keys (SSE-C), with keys generated and rotated by the security team.
- [x] C. Use SSE-KMS with a customer managed key whose key policy grants kms:Decrypt only to the application role, with automatic rotation enabled.
- [ ] D. Encrypt objects on the client side before upload, using keys that the security team stores in AWS Secrets Manager.

## Q02

A company uses AWS Organizations with 40 member accounts across several OUs. The security team must ensure that nobody in any member account, including each account's root user, can stop or delete the organization's AWS CloudTrail trails. The control must be preventive and require the least ongoing administration.

Which solution meets these requirements?

- [ ] A. In every member account, attach an IAM policy that denies cloudtrail:StopLogging and cloudtrail:DeleteTrail to all IAM users and roles.
- [ ] B. Create an SCP that explicitly denies cloudtrail:StopLogging and cloudtrail:DeleteTrail, and attach it to the organization root.
- [x] C. Replace the FullAWSAccess SCP on the organization root with an allow-list SCP that permits only CloudTrail read actions.
- [ ] D. Create an AWS Config rule that detects stopped trails and runs automatic remediation to restart logging.

## Q03

A three-tier application runs web servers in public subnets and database servers in private subnets. The web tier runs in an Auto Scaling group. The security team has found that the CIDR range 203.0.113.0/24 is sending malicious traffic to the web servers and must be blocked. The database servers must accept connections only from the web servers, even as web instances are launched and terminated. The public subnets use a custom network ACL whose rule 100 allows all inbound HTTPS traffic.

Which combination of actions meets these requirements? (Select TWO.)

- [ ] A. Add an inbound deny rule for 203.0.113.0/24 to the web tier's security group.
- [ ] B. Add an inbound deny rule for 203.0.113.0/24 with rule number 50 to the public subnets' network ACL.
- [ ] C. Add an inbound deny rule for 203.0.113.0/24 with rule number 200 to the public subnets' network ACL.
- [ ] D. Change the database security group to allow the database port from the web tier's security group.
- [ ] E. Change the database security group to allow the database port from the web instances' current private IP addresses.

## Q04

A company runs a licensing server on a single EBS-backed Amazon EC2 instance. Client software connects to the instance's private IP address, and the license is bound to the instance ID. The company wants the instance to recover automatically if the underlying host hardware fails, keeping the same instance ID, private IP address, and EBS volumes.

Which solution meets these requirements with the LEAST operational overhead?

- [ ] A. Create an Amazon CloudWatch alarm on the StatusCheckFailed_System metric with an EC2 recover action.
- [ ] B. Create an Amazon CloudWatch alarm on the StatusCheckFailed_Instance metric with an EC2 recover action.
- [ ] C. Place the instance in an Auto Scaling group with a minimum, maximum, and desired capacity of 1.
- [ ] D. Enable termination protection and set the instance's shutdown behavior to Stop.

## Q05

A company has stored 5 years of financial records in a versioned S3 bucket in eu-west-1. For disaster recovery, a solutions architect configured Cross-Region Replication to a new bucket in eu-central-1 yesterday. An audit today shows that newly uploaded objects are in the destination bucket, but none of the existing records are. The company needs every record in the destination bucket.

Which solution meets this requirement with the LEAST operational overhead?

- [ ] A. Enable S3 Replication Time Control (RTC) on the replication rule.
- [ ] B. Delete and recreate the replication rule so that it re-evaluates every object in the source bucket.
- [ ] C. Use S3 Batch Replication to replicate the existing objects to the destination bucket.
- [ ] D. Add a lifecycle rule to the source bucket that transitions the existing objects so that they generate replication events.

## Q06

To protect its backups if the production account is compromised, a company replicates an S3 bucket in its production account to a bucket in a separate backup account. Versioning is enabled on both buckets. The replication rule uses an IAM role in the production account whose permissions policy allows it to read from the source bucket and replicate objects to the destination bucket. Replication fails with Access Denied errors.

What should the solutions architect do to fix the replication?

- [ ] A. Add s3:* on the destination bucket to the replication role's permissions policy.
- [ ] B. Change the replication rule to transfer object ownership to the backup account.
- [ ] C. Create an IAM user in the backup account and add its access keys to the replication configuration.
- [ ] D. Add a bucket policy to the destination bucket that allows the replication role to replicate objects into it.

## Q07

A company runs a self-managed NoSQL database cluster on Amazon EC2. The database replicates every write to three nodes in different Availability Zones and automatically rebuilds any node that loses its data. Each node needs more than 300,000 random IOPS at the lowest possible latency.

Which storage option meets these requirements?

- [ ] A. Storage optimized instances that keep the database files on their NVMe instance store volumes.
- [ ] B. A single io2 Block Express EBS volume on each node, provisioned with the maximum IOPS.
- [ ] C. Several gp3 EBS volumes on each node, combined in a RAID 0 array.
- [ ] D. An Amazon EFS file system in Max I/O performance mode, shared by all nodes.

## Q08

A media company's users in Australia and Europe upload 2–4 GB video files directly to an S3 bucket named media-uploads-prod in us-east-1. Users complain that uploads are slow and that a network interruption forces the whole upload to start again.

Which combination of changes will improve upload speed and reliability? (Select TWO.)

- [ ] A. Enable S3 Transfer Acceleration on the bucket and upload through the accelerate endpoint.
- [ ] B. Generate S3 presigned URLs for the uploads.
- [ ] C. Upload the files using multipart upload.
- [ ] D. Add random hash prefixes to the object keys.
- [ ] E. Upload the files into the S3 One Zone-IA storage class.

## Q09

A company stores application logs in Amazon S3 as compressed daily archives of about 1 GB each. Logs are queried often during their first 30 days and afterwards only during occasional audits. Auditors accept a retrieval time of up to 5 hours. Logs must be deleted after 1 year.

Which lifecycle configuration is the MOST cost-effective?

- [ ] A. Transition objects to S3 Standard-IA after 30 days and expire them after 365 days.
- [ ] B. Transition objects to S3 Glacier Flexible Retrieval after 30 days and expire them after 365 days.
- [ ] C. Transition objects to S3 Glacier Deep Archive after 30 days and expire them after 365 days.
- [ ] D. Store objects in S3 Intelligent-Tiering and expire them after 365 days.

## Q10

A company runs a steady baseline of Amazon EC2 instances 24/7 and expects that baseline to continue for at least 3 years. Over the next year, the team plans to move several services from EC2 to AWS Fargate and AWS Lambda, and to change instance families as workloads are right-sized.

Which purchasing option provides the largest discount that continues to apply through these changes?

- [ ] A. Purchase 3-year Standard Reserved Instances for the current instance types.
- [ ] B. Run the baseline on Spot Instances.
- [ ] C. Purchase a 3-year EC2 Instance Savings Plan.
- [ ] D. Purchase a 3-year Compute Savings Plan.
