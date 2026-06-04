# AWS Cloud Practitioner Essentials

# Module 1: Introduction to the Cloud

Original servers

- need a lot of "workers" just incase there is a large number of customers/orders
- These large number of workers will end up playing/not doing work when the number of customers drop
- inefficient

AWS

- Provision/de-provision workers as and when you need
- only pay for what we use
- more cost efficient
- right configuration --> done automatically

Cloud computing?

- On-demand delivery of IT resources over the internet with pay-as-you-go pricing
  - on-demand --> use resources as needed
  - over the internet --> remote access
  - pay-as-you-go --> provision/de-provision
- Benefits?
  1. trade fixed expenses for variable expenses
  2. benefit from massive economies of sales
  3. stop guessing capacity
  4. Increase speed and agility
  5. no money spent on running & maintaining data centres
  6. can go global in minutes
     - deploy application in AWS serveice centres all around the world

Why is it reliable?

- A Region is a physical location around the world that contains multiple, isolated data centers. An Availability Zone consists of one or more discrete data centers, each with independent power, networking, and connectivity.
- Global infrastructure, where the data centers are located all around the world, not just one big center at one place
- it has multiple independent centers
- High availability
  - even if one component fails, other components can handle the job
- fault tolerance
  - even if multiple component fails, designed to be able to still be functional

Security?

- customer:
  - responsible of security in the cloud (data encription etc)
- AWS:
  - responsible of security of the cloud (physical security)

# Module 2: Compute in the Cloud (Amazon EC2)

Amazon Elastic Compute Cloud (compute-as-a-service)

- You need to the choose EC2 instance type (how powerful you want it) and the Amazon Machine Image (AMI), which determines the operating system and software for your instance.

- Multitenancy
  - sharing underlying hardware between virtual machines
- Configurations:
  - windows
  - linux
  - internal business apss
  - web apps
  - databases
  - third-party software

Instance Types

- grouped under instance families
  - general purpose
    - balanced resources
    - diverse workloads (web servers, code repositories)
    - good starting point
  - compute optimized
    - compute-intensive tasks
    - gaming servers
    - high performance computing (HPC)
    - scientific modeling
  - memory optimized
    - memory intensive tasks
  - accelerated computing
    - floating point number calculations
    - graphics processing
    - data pattern matching
    - hardware accelerators
  - storage optimized
    - high performance for locally stored data

- choose the instance type that provides necessary computing power and affordable

How to provision AWS Resources

- API: Application programming interface
- Interacting with AWS Services (via API)
  - AWS Management Console (learning phase)
    - visual & easy to digest
    - set up test environments
    - view AWS bills
    - view monitoring
    - work with non-technical resources
  - AWS Command Line Interface (CLI)
    - Make API calls using terminal
  - AWS Software Development Kit (SDK)
    - interact through various programming languages

Amazon EC2 Pricing

- On-Demand
  - pay only for compute capacity we consumed
- Savings Plan
- Reserved Instances
  - steady-state workload
- Spot Instances
  - bid on spare compute capacity at up to 90% off the On-Demand but might be interrupted when AWS reclaims the instance
- dedicated host
  - reserve entire physical server
  - for security sensitive work

Scaling EC2

- Scale out
  - horizontal scaling
  - add more resources so can get work done in parallel (aka more same workers)
- scale up
  - vertical scaling
  - adding more power to the machines that are running: more capability to individuals machines (aka more skilled worker)

Elastic Load Balancing

- distribute network traffic evenly
  - using Round Robin, Least connections, IP Hash and Least Response Time
- manage connection between backend instances and frontend instances
  - without ELB, every frontend instances must be connected to every backend instances
  - very complicated if there is a lot of instances
  - with ELB, each instances only have to be connected to one ELB, which handles/add connections based on network traffic
  - single point of contact for all incoming web traffic

Messaging and Queuing

- casher talks directly to barista when order received
  - tightly coupled architecture
    - if a single component fails/changes, it causes issues to other component/entire system
- casher post order received to an order board
  - loosely coupled architecture
  - Amazon Simple Queue Service (SQS)
    - send, store. receive messages
    - Payload: data stored within the messages
    - Amazon SQS queues: messages are placed until they are processed
  - Amazon Simple Notification Service (Amazon SNS)
    - a channel for messages to be delivered
    - need responses RIGHT NOW

# Module 3: Exploring Compute Services

Compute Options

- Unmanaged services (Amazon EC2)
  - AWS takes care of the underlying physical infrastructure, but users are responsible for setting up, securing and maintaining the virtual machine (OS, runtime, application)
- Managed services
  - AWS manages more of the stack (e.g. patching, scaling, monitoring)
  - e.g. Amazon RDS, Amazon ECS
- Fully managed / Serverless services
  - AWS manages everything — you only provide code or configuration
  - e.g. AWS Lambda, AWS Fargate

Serverless Computing

- cannot see or access the underlying infrastructure
- AWS Lambda (function as a service, any programming languages)
  - upload your code → set a trigger → Lambda runs your code only when triggered
  - Lambda handles provisioning, scaling, and server management automatically
  - pay only for compute time while the code is actually running (rounded to the nearest millisecond)
  - ideal for short-running tasks (< 15 minutes), event-driven workloads (e.g. image uploads, API calls, database changes)
  - Example triggers: HTTP requests via API Gateway, S3 events, DynamoDB streams, scheduled CloudWatch events

Container Services

- Containers
  - package your application code + dependencies + configuration into a single portable unit (Docker image)
  - consistent environment across development, testing, and production
  - more lightweight than a full VM — share the host OS kernel
- Amazon Elastic Container Service (ECS)
  - streamlined and integrated, define some parameteres
  - highly scalable, high-performance container management system
  - supports Docker containers
  - you define tasks (what to run) and services (how many copies, load balancing)
  - you still manage the underlying EC2 instances unless you use Fargate
- Amazon Elastic Kubernetes Service (EKS)
  - open source, more complex, more control and flexibility
  - run fully managed Kubernetes clusters on AWS
  - good choice if your team already uses Kubernetes or needs fine-grained orchestration control
- Amazon Elastic Container Registry (ECR)
  - fully managed Docker container registry — store, manage, and deploy container images
  - works natively with ECS, EKS, and Fargate (no extra auth setup needed)
  - images are stored privately by default; can be made public via ECR Public Gallery
  - integrates with IAM for fine-grained access control
  - supports image vulnerability scanning to detect security issues before deployment
  - typical workflow: build image → push to ECR → ECS/EKS/Fargate pulls and runs it
- AWS Fargate
  - serverless compute engine for containers — works with both ECS and EKS
  - no need to provision or manage EC2 instances; just define CPU/memory requirements and deploy
  - pay only for the resources your containers actually use
  - removes the operational overhead of managing a cluster

When to use what?

| Scenario                                 | Recommended Service |
| ---------------------------------------- | ------------------- |
| Full control over OS & runtime           | Amazon EC2          |
| Short event-driven functions             | AWS Lambda          |
| Containerised apps, manage own servers   | Amazon ECS on EC2   |
| Containerised apps, no server management | AWS Fargate         |
| Existing Kubernetes workloads            | Amazon EKS          |

Putting it together

- start with uploading container image to ECR
- choose serveice based on needs: ECS or EKS
- Select which compute platform to run container: EC2 or Fargate

Additional Compute Services

- AWS Elastic Beanstalk
  - simplified procisioning
  - configuration management
  - visibility and control
- AWS Batch
  - fully managed service for running batch computing jobs at any scale
  - you define the job (Docker container + compute requirements); Batch provisions the right amount of EC2/Spot instances and runs the jobs
  - automatically scales compute up when jobs are queued, scales back down when done
  - ideal for: data processing pipelines, ML model training, financial simulations, image rendering
  - pay only for the compute resources used while jobs are running
  - infrastructure management
  - parallel processing support
  - automatic scaling
- Amazon Lightsail
  - simplified cloud platform for small projects and beginners
  - cost-effective
  - managed infastructure
  - bundles compute, storage, DNS, and networking into fixed low-cost monthly plans
  - pre-configured application stacks (WordPress, LAMP, Node.js, etc.) launchable in one click
  - good for: simple websites, blogs, small web apps, dev/test environments
  - less flexible than EC2 but much lower barrier to entry
- AWS Outposts
  - hybrid cloud solution
  - consistent environments
  - low latency and data recidency
  - brings AWS infrastructure and services physically into your on-premises data center
  - fully managed by AWS — same hardware, APIs, and tools as the AWS cloud
  - use cases: data residency requirements, ultra-low latency to on-premises systems, regulatory compliance
  - allows hybrid workloads where some data/processing must stay on-premises

# Module 4: Going Global

AWS Global Infrastructure

- Region
  - physical location around the world that contains multiple, isolated Availability Zones
  - currently 30+ Regions globally
  - regions are completely independent — data does not leave a Region unless you explicitly move it
- Availability Zone (AZ)
  - one or more discrete data centers within a Region, each with independent power, networking, and connectivity
  - multiple AZs per Region provide high availability and fault tolerance
  - best practice: deploy across at least 2 AZs
- Edge Locations
  - separate from Regions and AZs — smaller caching endpoints distributed globally
  - used by Amazon CloudFront and Route 53 to serve content close to users
  - there are far more Edge Locations than Regions (400+)
  - located outside of AWS Regions

Choosing a Region

- Compliance
  - data follows local laws of where the region lives (e.g. GDPR requires EU data to stay in EU)
- Proximity
  - choose the region closest to your customer base to reduce latency
- Feature availability
  - not all AWS services/features are available in every Region; check before committing
- Pricing
  - costs vary between Regions — same service can be cheaper in one region vs another

Amazon CloudFront (CDN)

- Content Delivery Network — caches content at Edge Locations around the world
- reduces latency by serving content from the Edge Location closest to the user
- works with S3, EC2, ELB, and custom origins
- also provides DDoS protection via AWS Shield integration

Amazon Route 53 (DNS)

- highly available and scalable Domain Name System (DNS) service
- translates domain names (e.g. example.com) into IP addresses
- also handles domain registration
- Routing policies:
  - Simple: route to a single resource
  - Weighted: split traffic across multiple resources by percentage
  - Latency-based: route to the Region with lowest latency for the user
  - Failover: route to a backup resource if the primary is unhealthy
  - Geolocation: route based on user's geographic location

Cloud Formation

- supports infrastructure as code (IaC), enabling consistent, repeateable deployments across different environments
- designed to handle complex setups.
- defines infrastructure as code to help make sure that deployments are consistent across different environments such as development, testing, and production.
- With CloudFormation, users can model and set up their AWS resources using code to automate provisioning and the management of infrastructure
  - This method can help to reduce errors and maintain consistency across environments.

# Module 5: Networking

Amazon Virtual Private Cloud (VPC)

- logically isolated section of the AWS Cloud — your own private network
- you define the IP address range, subnets, route tables, and gateways
- resources inside a VPC are not accessible from the internet by default

Subnets

- Public subnet
  - has a route to an Internet Gateway → resources can communicate with the internet
  - e.g. web servers, load balancers
- Private subnet
  - no direct internet access
  - e.g. databases, internal application servers

Gateways and Connections

- Internet Gateway (IGW)
  - attaches to a VPC to allow traffic between the VPC and the internet
  - required for resources in public subnets to be reachable
- Virtual Private Gateway
  - entry point for encrypted VPN connections from on-premises networks into the VPC
  - traffic still travels over the public internet but is encrypted
- AWS Direct Connect
  - dedicated private physical connection from on-premises data center to AWS
  - not over the public internet → lower latency, more consistent bandwidth
  - good for high-throughput or compliance-sensitive workloads

Network Traffic Filtering

- Network Access Control Lists (NACLs)
  - stateless: evaluates both inbound AND outbound rules independently
  - applied at the subnet level — affects all resources within the subnet
  - rules are evaluated in order (lowest number first); default allows all traffic
- Security Groups
  - stateful: if inbound traffic is allowed, the response is automatically allowed out
  - applied at the instance/resource level
  - default: deny all inbound, allow all outbound
  - you add rules to explicitly allow traffic (cannot explicitly deny)

| Feature | NACLs     | Security Groups  |
| ------- | --------- | ---------------- |
| Level   | Subnet    | Instance         |
| State   | Stateless | Stateful         |
| Default | Allow all | Deny all inbound |

# Module 6: Storage

Amazon Simple Storage Service (S3)

- object storage — store any type of data as objects inside buckets
- each object = data + metadata + unique key
- virtually unlimited storage; maximum single object size is 5 TB
- highly durable: data is automatically replicated across multiple AZs
- Storage classes (choose based on access frequency):
  - S3 Standard: frequently accessed data; high durability, stored across ≥3 AZs
  - S3 Standard-IA (Infrequent Access): lower storage cost, retrieval fee applies
  - S3 One Zone-IA: stored in a single AZ; cheaper, but less resilient
  - S3 Intelligent-Tiering: automatically moves objects between tiers based on access patterns
  - S3 Glacier Instant Retrieval: archive data, millisecond retrieval
  - S3 Glacier Flexible Retrieval: archive, retrieval in minutes to hours
  - S3 Glacier Deep Archive: lowest cost; retrieval within 12 hours; long-term retention

Amazon Elastic Block Store (EBS)

- block storage volumes attached to EC2 instances (like a hard drive for a server)
- data persists independently from the EC2 instance lifecycle
- can only be attached to one EC2 instance at a time (within the same AZ)
- EBS Snapshots: point-in-time backups stored in S3; incremental (only changed blocks)

Amazon Elastic File System (EFS)

- managed NFS (Network File System) — shared file storage
- multiple EC2 instances across multiple AZs can read/write simultaneously
- scales automatically as files are added or removed — no provisioning needed
- good for shared content, home directories, CMS workloads

Additional Storage Services

- AWS Storage Gateway: hybrid storage — connects on-premises environments to AWS cloud storage
- AWS Snow Family: physical devices for moving large amounts of data into/out of AWS when network transfer is impractical
  - Snowcone: smallest, portable (up to 14 TB)
  - Snowball Edge: larger (up to 80 TB), can run compute at edge locations
  - Snowmobile: exabyte-scale data transfer via a shipping container

# Module 7: Databases

Amazon Relational Database Service (RDS)

- fully managed relational database service
- handles patching, backups, failover, and scaling automatically
- supported engines: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Amazon Aurora
- Multi-AZ deployment: automatic standby replica in another AZ for high availability

Amazon Aurora

- AWS-built relational database; MySQL and PostgreSQL compatible
- up to 5× faster than standard MySQL, 3× faster than PostgreSQL
- replicates 6 copies of data across 3 AZs automatically
- storage auto-scales up to 128 TB
- good choice when you need high performance and AWS-native integration

Amazon DynamoDB

- fully managed, serverless NoSQL key-value and document database
- single-digit millisecond response times at any scale
- automatically scales throughput up and down based on demand
- no schema — flexible data structure per item
- good for high-traffic web apps, gaming leaderboards, IoT data

Amazon Redshift

- managed data warehousing service for large-scale analytics
- designed for OLAP (Online Analytical Processing), not transactional workloads
- can query petabytes of structured data
- integrates with BI tools (Tableau, QuickSight)

AWS Database Migration Service (DMS)

- migrate databases to AWS with minimal downtime
- source database remains fully operational during migration
- supports homogeneous migrations (e.g. MySQL → RDS MySQL) and heterogeneous (e.g. Oracle → Aurora)
- also used for continuous data replication and database consolidation

# Module 8: AI ML and Data Analytics

# Module 9: Security

Shared Responsibility Model (revisited)

- AWS: security OF the cloud (physical hardware, global infrastructure, managed service software)
- Customer: security IN the cloud (data, IAM config, OS patching on EC2, encryption choices)
- boundary shifts depending on service type — more managed = AWS takes more responsibility

AWS Identity and Access Management (IAM)

- Root user
  - created when you first open an AWS account
  - has full access to everything — do NOT use for everyday tasks
  - enable MFA on root user immediately
- IAM Users
  - individual identities with credentials (username/password or access keys)
  - by default, a new IAM user has NO permissions
- IAM Groups
  - collection of IAM users
  - attach policies to the group — all members inherit those permissions
- IAM Roles
  - temporary identity assumed by a user, service, or application
  - no permanent credentials — permissions are granted only while the role is assumed
  - e.g. EC2 instance assumes a role to access S3 without hardcoding credentials
- IAM Policies
  - JSON documents that define allow/deny permissions for actions on resources
  - principle of least privilege: grant only the permissions needed, nothing more
- Multi-Factor Authentication (MFA)
  - adds a second verification step (e.g. OTP from an authenticator app)
  - should be enabled on root user and all privileged IAM users

AWS Organizations

- centrally manage multiple AWS accounts under one organisation
- consolidated billing: single payment method for all accounts, volume discounts apply
- Service Control Policies (SCPs): set permission guardrails across accounts or Organisational Units (OUs)
  - SCPs do not grant permissions — they restrict what accounts can do even if IAM allows it
- Organisational Units (OUs): group accounts by team, environment, or business unit (e.g. Dev OU, Prod OU)

Threat Detection and Protection

- AWS Shield
  - protects against DDoS attacks
  - Shield Standard: automatically enabled for all AWS customers, no extra cost
  - Shield Advanced: paid tier; enhanced protection, 24/7 DDoS response team, cost protection
- AWS WAF (Web Application Firewall)
  - filters malicious HTTP/S traffic before it reaches your application
  - blocks SQL injection, cross-site scripting (XSS), and custom rules
  - works with CloudFront, ALB, API Gateway
- Amazon GuardDuty
  - intelligent threat detection using ML
  - continuously monitors CloudTrail logs, VPC Flow Logs, and DNS logs
  - detects things like unusual API calls, compromised instances, crypto-mining activity
- Amazon Inspector
  - automated security assessments for EC2 instances and container images
  - checks for software vulnerabilities and unintended network exposure
- Amazon Macie
  - uses ML to discover, classify, and protect sensitive data in S3
  - identifies PII (Personally Identifiable Information) and alerts on unusual access

Encryption

- AWS Key Management Service (KMS)
  - create, manage, and control encryption keys
  - integrates with most AWS services (S3, EBS, RDS, etc.)
  - you control who can use which keys
- Encryption at rest: data encrypted when stored (S3, EBS snapshots, RDS)
- Encryption in transit: data encrypted while moving (TLS/SSL)

# Module 10: Monitoring, Compliance and Governance in the AWS Cloud

Amazon CloudWatch

- collect and track metrics from AWS resources and applications
- set Alarms: trigger notifications or automated actions when a metric crosses a threshold
  - e.g. alert when CPU > 80%, or auto-scale when request count spikes
- CloudWatch Logs: collect, store, and search log files from EC2, Lambda, and other services
- CloudWatch Dashboards: customisable real-time views of your metrics
- CloudWatch Events / Amazon EventBridge: respond to state changes in AWS resources with automated actions

AWS CloudTrail

- records every API call made in your account (who, what, when, from where)
- key distinction from CloudWatch: CloudWatch = performance metrics; CloudTrail = who did what
- Management events: operations on resources (e.g. create EC2, delete S3 bucket)
- Data events: object-level operations (e.g. S3 GetObject, Lambda invocations)
- logs stored in S3; used for auditing, incident investigation, and compliance
- CloudTrail Insights: automatically detects unusual API activity

AWS Artifact

- on-demand access to AWS compliance reports (SOC, ISO, PCI DSS, HIPAA, etc.)
- also used to review and manage compliance agreements (e.g. BAA for HIPAA)
- no cost — available to all AWS customers

AWS Trusted Advisor

- automated tool that inspects your AWS environment and recommends improvements
- checks across 5 categories:
  1. Cost Optimisation: identify idle resources, unused reserved instances
  2. Performance: check service limits, EC2 usage patterns
  3. Security: open S3 buckets, unrestricted security group rules, MFA on root
  4. Fault Tolerance: Multi-AZ usage, EBS snapshot age, auto scaling groups
  5. Service Limits: warn when approaching AWS account limits
- Basic checks: free for all accounts
- Full checks: require Business or Enterprise Support plan

AWS X-Ray

- trace and analyse requests as they travel through distributed applications
- helps identify bottlenecks and errors across microservices, Lambda, and APIs
- generates a service map showing how components interact and where latency occurs

Amazon EventBridge

- serverless event bus — routes events between AWS services, SaaS apps, and custom apps
- replaces and extends CloudWatch Events
- event sources: AWS services, custom applications, partner SaaS (e.g. Zendesk, Shopify)
- you define rules that match events and route them to targets (Lambda, SQS, Step Functions, etc.)

# Module 11: Pricing and Support

# Module 12: Migrating to the AWS Cloud

# Module 13: Well-Architected Solutions
