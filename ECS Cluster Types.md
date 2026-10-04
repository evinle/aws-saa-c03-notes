- EC2 mode and Fargate mode
	- Determines how much admin overhead

- ECS management components
	- SchedulingAndOrchestration
	- ClusterManager
	- PlacementEngine
# EC2 Mode
- ECS Cluster uses an Auto Scaling Group (ASG) to provision EC2 instances in your selected AZ and in the number that you specified
- It is not serverless, you pay for it as if it's running EC2 instances
- More control but also more management overhead
- ![[Pasted image 20261004213603.png]]

# Fargate Mode
- Tasks and Services are run on shared Fargate Infrastructure
	- They're injected into YOUR VPC by getting assigned an ENI
	- So you could make them private/public/assign IPs/SGs
- You only pay for the containers that you're using

# EC2 vs ECS (EC2) vs Fargate
- If you use containers ... ECS
- Large workload - price conscious - EC2 Mode
- Large workload - overhead conscious - Fargate Mode
- Small / Burst workloads - Fargate Mode
- Batch / Periodic workloads - Fargate Mode
