# SAA-C03 Exam Guide (condensed)

Source: official AWS exam guide PDF `solutions-architect-associate-03.pdf` (© 2026), transcribed 2026-10-18.
Online: https://docs.aws.amazon.com/aws-certification/latest/examguides/solutions-architect-associate-03.html
If AWS revises the guide, re-transcribe this file and update the date.

## Exam facts

- 65 questions: 50 scored + 15 unscored (unscored are not identified)
- 130 minutes
- Scaled score 100–1,000, pass = 720. Compensatory: no per-domain minimum
- Unanswered = wrong, no penalty for guessing
- Response types:
  - **Multiple choice**: 1 correct, 3 distractors
  - **Multiple response**: 2+ correct out of 5+ options
- Distractors are "response options that a candidate with incomplete knowledge or skill might choose" and are "generally plausible responses that match the content area"
- Services appear by official short name (e.g. "Amazon SNS", not the full name)

## Domains and weights

| # | Domain | Weight |
|---|---|---|
| 1 | Design Secure Architectures | 30% |
| 2 | Design Resilient Architectures | 26% |
| 3 | Design High-Performing Architectures | 24% |
| 4 | Design Cost-Optimized Architectures | 20% |

## Domain 1: Design Secure Architectures (30%)

### Task 1.1: Design secure access to AWS resources
Knowledge: access controls across multiple accounts; federated access and identity services (IAM, IAM Identity Center); global infrastructure (AZs, Regions); security best practices (least privilege); shared responsibility model.
Skills:
- Security best practices for IAM users and root users (MFA)
- Flexible authorization model with IAM users, groups, roles, policies
- Role-based access control (AWS STS, role switching, cross-account access)
- Multi-account security strategy (Control Tower, SCPs)
- When to use resource policies for AWS services
- When to federate a directory service with IAM roles

### Task 1.2: Design secure workloads and applications
Knowledge: application configuration and credentials security; AWS service endpoints; control ports, protocols, network traffic; secure application access; security services and use cases (Cognito, GuardDuty, Macie); external threat vectors (DDoS, SQL injection).
Skills:
- VPC architectures with security components (security groups, route tables, NACLs, NAT gateways)
- Network segmentation (public vs private subnets)
- Integrating services to secure apps (Shield, WAF, IAM Identity Center, Secrets Manager)
- Securing external connections (VPN, Direct Connect)

### Task 1.3: Determine appropriate data security controls
Knowledge: data access and governance; data recovery; data retention and classification; encryption and key management.
Skills:
- Aligning AWS technologies to compliance requirements
- Encryption at rest (KMS)
- Encryption in transit (ACM, TLS)
- Access policies for encryption keys
- Data backups and replication
- Policies for data access, lifecycle, protection
- Rotating keys and renewing certificates

## Domain 2: Design Resilient Architectures (26%)

### Task 2.1: Design scalable and loosely coupled architectures
Knowledge: API creation and management (API Gateway, REST); managed services and use cases (Transfer Family, SQS, Secrets Manager); caching strategies; microservice design (stateless vs stateful); event-driven architectures; horizontal vs vertical scaling; edge accelerators (CDN); migrating apps into containers; load balancing (ALB); multi-tier architectures; queuing and messaging (pub/sub); serverless (Fargate, Lambda); storage types (object, file, block); container orchestration (ECS, EKS); when to use read replicas; workflow orchestration (Step Functions).
Skills:
- Event-driven, microservice, multi-tier designs from requirements
- Scaling strategies per component
- Services needed for loose coupling
- When to use containers; when to use serverless
- Recommending compute, storage, networking, database from requirements
- Purpose-built services for workloads

### Task 2.2: Design highly available and/or fault-tolerant architectures
Knowledge: global infrastructure (AZs, Regions, Route 53); managed AI services and use cases (Comprehend, Polly); basic networking (route tables); DR strategies (backup and restore, pilot light, warm standby, active-active, RPO, RTO); distributed design patterns; failover strategies; immutable infrastructure; load balancing (ALB); proxies (RDS Proxy); service quotas and throttling (quotas in a standby environment); storage durability and replication; workload visibility (X-Ray).
Skills:
- Automation strategies for infrastructure integrity
- Services for HA/FT across Regions or AZs
- Metrics from business requirements for HA
- Removing single points of failure
- Data durability and availability (backups)
- Choosing a DR strategy for business requirements
- Improving reliability of legacy apps when code changes aren't possible
- Purpose-built services for workloads

## Domain 3: Design High-Performing Architectures (24%)

### Task 3.1: High-performing and/or scalable storage
Knowledge: hybrid storage; storage services and use cases (S3, EFS, EBS); storage types (object, file, block).
Skills: storage services and configurations that meet performance demands; storage that scales for future needs.

### Task 3.2: High-performing and elastic compute
Knowledge: compute services and use cases (Batch, EMR, Fargate); distributed computing with global infrastructure and edge; queuing and messaging (pub/sub); scalability (EC2 Auto Scaling, AWS Auto Scaling); serverless (Lambda, Fargate); container orchestration (ECS, EKS).
Skills: decoupling so components scale independently; metrics and conditions for scaling actions; compute options and features (instance types); resource type and size (Lambda memory).

### Task 3.3: High-performing databases
Knowledge: global infrastructure; caching (ElastiCache); access patterns (read- vs write-intensive); capacity planning (capacity units, instance types, Provisioned IOPS); connections and proxies; engines and use cases (heterogeneous vs homogeneous migrations); replication (read replicas); database types (serverless, relational vs non-relational, in-memory).
Skills: configuring read replicas; designing database architectures; choosing an engine (MySQL vs PostgreSQL); choosing a type (Aurora, DynamoDB); integrating caching.

### Task 3.4: High-performing and/or scalable networks
Knowledge: edge networking (CloudFront, Global Accelerator); network design (subnet tiers, routing, IP addressing); load balancing (ALB); connection options (VPN, Direct Connect, PrivateLink).
Skills: topologies (global, hybrid, multi-tier); configurations that scale; resource placement; load-balancing strategy.

### Task 3.5: High-performing data ingestion and transformation
Knowledge: analytics and visualization (Athena, Lake Formation, Amazon Quick); ingestion patterns (frequency); data transfer (DataSync, Storage Gateway); transformation (Glue); securing ingestion access points; sizes and speeds; streaming (Kinesis).
Skills: building and securing data lakes; streaming architectures; data transfer solutions; visualization; compute for data processing (EMR); ingestion configuration; format transformation (.csv to .parquet).

## Domain 4: Design Cost-Optimized Architectures (20%)

Every task in this domain also lists: cost management features (cost allocation tags, multi-account billing) and tools (Cost Explorer, Budgets, Cost and Usage Report).

### Task 4.1: Cost-optimized storage
Knowledge: access options (S3 Requester Pays); storage services and use cases (FSx, EFS, S3, EBS); backup strategies; block storage options (HDD vs SSD volume types); data lifecycles; hybrid storage (DataSync, Transfer Family, Storage Gateway); access patterns; tiering (cold tiers for objects); storage types.
Skills: storage strategies (batch vs individual S3 uploads); right-sizing storage; lowest-cost transfer into AWS; when storage auto scaling is needed; S3 lifecycles; backup and archival choice; migration service choice; storage tier choice; data lifecycle choice; most cost-effective storage service.

### Task 4.2: Cost-optimized compute
Knowledge: global infrastructure; purchasing options (Spot, Reserved, Savings Plans); distributed compute (edge processing); hybrid compute (Outposts); instance types, families, sizes (memory/compute optimized, virtualization); utilization optimization (containers, serverless, microservices); scaling (auto scaling, hibernation).
Skills: load-balancing strategy (ALB L7 vs NLB L4 vs GWLB); scaling methods (horizontal vs vertical, hibernation); cost-effective compute (Lambda vs EC2 vs Fargate); availability for workload classes (prod vs non-prod); instance family; instance size.

### Task 4.3: Cost-optimized databases
Knowledge: caching; data retention; capacity planning (capacity units); connections and proxies; engines and migrations; replication (read replicas); database types (relational vs non-relational, Aurora, DynamoDB).
Skills: backup and retention (snapshot frequency); engine choice; cost-effective database services (DynamoDB vs RDS, serverless); cost-effective formats (time series, columnar); migrating schemas and data across locations or engines.

### Task 4.4: Cost-optimized networks
Knowledge: load balancing (ALB); NAT gateways (NAT instance vs NAT gateway cost); connectivity (private lines, dedicated lines, VPNs); routing, topology, peering (Transit Gateway, VPC peering); network services (DNS).
Skills: NAT gateway layout (one shared vs one per AZ); connection choice (Direct Connect vs VPN vs internet); routes that minimize transfer cost (Region-to-Region, AZ-to-AZ, private-to-public, Global Accelerator, VPC endpoints); when CDNs and edge caching pay off; reviewing workloads for network savings; throttling strategy; bandwidth sizing (one vs multiple VPNs, Direct Connect speed).

## In-scope services (non-exhaustive)

- **Analytics**: Athena, Data Exchange, Data Firehose, EMR, Glue, Kinesis, Lake Formation, MSK, OpenSearch Service, Amazon Quick, Redshift
- **Application Integration**: AppFlow, EventBridge, MQ, SNS, SQS, Step Functions
- **Cost Management**: Budgets, Cost and Usage Report, Cost Explorer, Savings Plans
- **Compute**: Batch, EC2, EC2 Auto Scaling, Elastic Beanstalk, Outposts, Serverless Application Repository, VMware Cloud on AWS, Wavelength
- **Containers**: ECR, ECS, ECS Anywhere, EKS, EKS Anywhere, EKS Distro
- **Database**: Aurora, Aurora Serverless, DocumentDB, DynamoDB, ElastiCache, Keyspaces, Neptune, RDS, Redshift
- **Developer Tools**: X-Ray
- **Front-End Web and Mobile**: Amplify, API Gateway, Device Farm
- **Machine Learning**: Comprehend, Lex, Polly, Rekognition, SageMaker AI, Textract, Transcribe, Translate
- **Management and Governance**: AWS Auto Scaling, CLI, CloudFormation, CloudTrail, CloudWatch, Compute Optimizer, Config, Control Tower, Health Dashboard, License Manager, Managed Grafana, Managed Service for Prometheus, Management Console, Organizations, Service Catalog, Systems Manager, Trusted Advisor, Well-Architected Tool
- **Media Services**: Elastic Transcoder, Kinesis Video Streams
- **Migration and Transfer**: Application Migration Service, DataSync, DMS, Snow Family, Transfer Family
- **Networking and Content Delivery**: Client VPN, CloudFront, Direct Connect, ELB, Global Accelerator, PrivateLink, Route 53, Site-to-Site VPN, Transit Gateway, VPC
- **Security, Identity, and Compliance**: Artifact, ACM, CloudHSM, Cognito, Detective, Directory Service, Firewall Manager, GuardDuty, IAM Identity Center, Inspector, KMS, Macie, Network Firewall, RAM, Secrets Manager, Security Hub, Shield, WAF, IAM
- **Serverless**: Fargate, Lambda
- **Storage**: Backup, EBS, EFS, FSx (all types), S3, S3 Glacier, Storage Gateway

## Out-of-scope services (never write questions on these)

MWAA; Sumerian; Managed Blockchain; Lightsail; RDS on VMware; CDK, CloudShell, CodeArtifact, CodeBuild, CodeCommit, CodeDeploy, Corretto, Fault Injection Simulator, Tools and SDKs; Location Service; GameLift; all IoT services; MXNet, DeepComposer, Deep Learning AMIs and Containers, DevOps Guru, Elastic Inference, HealthLake, Inferentia, Personalize, PyTorch/TensorFlow on AWS; Console Mobile App, Distro for OpenTelemetry; all Elemental services, IVS; Migration Evaluator; Cloud Map; Braket; Ground Station.
