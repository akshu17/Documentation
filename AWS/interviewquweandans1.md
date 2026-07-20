1. What is AWS?
Answer
AWS (Amazon Web Services) is a cloud computing platform that provides on-demand services like compute, storage, networking, databases, security, monitoring, and DevOps tools. It follows a pay-as-you-go pricing model.

2. What is a VPC?
Answer
A Virtual Private Cloud (VPC) is a logically isolated virtual network where we deploy AWS resources like EC2, RDS, and Load Balancers. It gives us control over IP ranges, subnets, route tables, security, and internet connectivity.

3. What are the components of a VPC?
Answer
VPC
CIDR Block
Public Subnet
Private Subnet
Route Table
Internet Gateway (IGW)
NAT Gateway
Security Groups
Network ACLs
Elastic IP
VPC Endpoints (optional)

4. Difference between Security Group and Network ACL?

Security Group	Network ACL
Instance-level firewall	Subnet-level firewall
Stateful	Stateless
Supports Allow rules only	Supports Allow and Deny rules
Applied to EC2 instances	Applied to subnets

5. What is an Internet Gateway?
Answer
An Internet Gateway (IGW) enables communication between a VPC and the internet. It is attached to the VPC, and the public subnet's route table points to it.

6. What is a NAT Gateway?
Answer
A NAT Gateway allows instances in a private subnet to access the internet for updates or downloads while preventing inbound internet connections.

7. What is EC2?
Answer
Amazon EC2 (Elastic Compute Cloud) is a virtual server that allows users to run applications in the AWS cloud.

8. What is an AMI?
Answer
An Amazon Machine Image (AMI) is a template that contains:
Operating System
Installed software
Configuration
It is used to launch EC2 instances.

9. What is Auto Scaling?
Answer
Auto Scaling automatically adds or removes EC2 instances based on demand using CloudWatch metrics and scaling policies.

10. What is an Auto Scaling Group (ASG)?
Answer
An Auto Scaling Group manages EC2 instances by maintaining the desired number of healthy instances and replacing unhealthy ones automatically.

11. What is an Application Load Balancer (ALB)?
Answer
An ALB distributes incoming HTTP/HTTPS traffic across multiple EC2 instances, improving availability and fault tolerance.

12. What is Amazon S3?
Answer
Amazon S3 is an object storage service used to store files, backups, logs, images, videos, and application data with high durability and scalability.

13. How do you make an S3 bucket private?
Answer
Enable Block Public Access
Remove public bucket policies
Remove public ACLs
Use IAM roles or bucket policies for access

14. What is Versioning in S3?
Answer
Versioning stores multiple versions of an object, allowing recovery from accidental deletion or overwrites.

15. What is Cross-Region Replication (CRR)?
Answer
CRR automatically replicates new objects from a source S3 bucket to a destination bucket in another AWS Region. Versioning must be enabled on both buckets.

16. Does CRR copy existing objects?
Answer
No. Existing objects are not copied automatically. Use S3 Batch Replication to replicate existing objects.

17. What is S3 Transfer Acceleration?
Answer
S3 Transfer Acceleration speeds up uploads and downloads by routing traffic through the nearest AWS Edge Location and then over the AWS global private network.

18. What is EBS?
Answer
Amazon Elastic Block Store (EBS) provides persistent block storage volumes for EC2 instances.

19. Difference between EBS and S3?
EBS	S3
Block Storage	Object Storage
Attached to EC2	Accessed via API
Low latency	Highly scalable
Used for OS and databases	Used for files and backups

20. What is RDS?
Answer
Amazon RDS is a managed relational database service that supports MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora.

21. What is a Read Replica?
Answer
A Read Replica is a read-only copy of an RDS database used to offload read traffic. It uses asynchronous replication.

22. Difference between Read Replica and Multi-AZ?
Read Replica	Multi-AZ
Read scaling	High availability
Asynchronous replication	Synchronous replication
No automatic failover	Automatic failover

23. What is AWS Lambda?
Answer
AWS Lambda is a serverless compute service that runs code without managing servers. It executes functions in response to events.

24. What is IAM?
Answer
AWS Identity and Access Management (IAM) controls authentication and authorization using users, groups, roles, and policies.

25. Difference between IAM User and IAM Role?
IAM User	IAM Role
Permanent identity	Temporary identity
Used by humans	Used by AWS services and applications
Uses access keys	Uses temporary credentials

26. How do you manage credentials?
Answer
Use IAM Roles for AWS services.
Store secrets in AWS Secrets Manager.
Store configuration in Parameter Store.
Use AWS STS for temporary credentials.
Never hardcode credentials.

27. What is CloudWatch?
Answer
Amazon CloudWatch monitors AWS resources and applications. It collects metrics, logs, and events, and triggers alarms and Auto Scaling actions.

28. What is CloudTrail?
Answer
AWS CloudTrail records API calls and user activity for auditing, governance, and troubleshooting.

29. Difference between CloudWatch and CloudTrail?
CloudWatch	CloudTrail
Monitoring	Auditing
Metrics and Logs	API activity
Performance	Security and compliance

30. What is Route 53?
Answer
Amazon Route 53 is a managed DNS service used for domain registration, DNS routing, health checks, and traffic management.

31. What is an Elastic IP?
Answer
An Elastic IP is a static public IPv4 address that can be associated with an EC2 instance and remapped if needed.

32. What is a Launch Template?
Answer
A Launch Template defines EC2 configuration such as:
AMI
Instance Type
Security Group
IAM Role
User Data
It is used by Auto Scaling Groups.

33. What happens if an EC2 instance becomes unhealthy in an ASG?
Answer
The Auto Scaling Group detects the unhealthy instance using health checks, terminates it, launches a new instance, and registers it with the Load Balancer.

34. How do you troubleshoot an EC2 instance that is down?
Answer
Check EC2 state
Verify System and Instance Status Checks
Check Security Groups
Verify NACLs and Route Tables
Check CPU, memory, and disk usage
Review application logs
Use CloudWatch metrics
Restart or replace the instance if required

35. What is the AWS Shared Responsibility Model?
Answer
AWS is responsible for security of the cloud (physical infrastructure, networking, hardware), while customers are responsible for security in the cloud (data, IAM, OS patching, application security, configurations).

Interview Tips
Explain concepts with a real-world example.
Mention AWS best practices (IAM Roles, least privilege, MFA, encryption).
When asked scenario-based questions, explain your troubleshooting steps in order.
If discussing production environments, mention Auto Scaling, Load Balancer, CloudWatch, and CloudTrail where relevant.

