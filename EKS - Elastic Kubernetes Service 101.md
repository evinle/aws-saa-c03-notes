- Kubernetes as a Service
- AWS Managed Kubernetes - open source & cloud agnostic
- On AWS, AWS Outposts (tiny AWS on prem), EKS Anywhere (EKS clusters on premise), EKS Distro (Open source EKS)
- Control plane managed by AWS
	- Scales based on load, runs on multiple AZs
- Integrates with AWS Services ... ECR, ELB, IAM, VPC
- EKS Cluster = EKS Control Plane + EKS Nodes
- etcd distributed across multiple AZs
- Nodes - self managed (EC2 instances you manage), Managed node groups (EC2, provisioning and lifecycle handled), Fargate pods (no instances), similar to ECS fargate
- Windows, GPU, Inferentia, Bottlerocket, Outposts, Local zones... check node type
- Storage Providers - EBS, EFS, FSx for  persistent storage

	![[Pasted image 20261015223039.png]]h