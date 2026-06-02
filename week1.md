# AWS Cloud Practitioner Essentials

# Module 1

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

# Module 3: Exploring Compute Servives

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

# Module 4: Networking

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

| Feature | NACLs | Security Groups |
|---|---|---|
| Level | Subnet | Instance |
| State | Stateless | Stateful |
| Default | Allow all | Deny all inbound |

Amazon Route 53 (DNS)

- highly available and scalable Domain Name System (DNS) service
- translates domain names (e.g. example.com) into IP addresses
- also handles domain registration
- Routing policies:
  - Simple: route to a single resource
  - Weighted: split traffic across multiple resources by percentage
  - Latency-based: route to the region with lowest latency for the user
  - Failover: route to a backup resource if the primary is unhealthy
  - Geolocation: route based on user's geographic location

Amazon CloudFront (CDN)

- Content Delivery Network — caches content at Edge Locations around the world
- reduces latency by serving content from the location closest to the user
- works with S3, EC2, ELB, and custom origins
- also provides DDoS protection via AWS Shield integration

# Module 5: Storage and Databases

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

Additional Storage Services

- AWS Storage Gateway: hybrid storage — connects on-premises environments to AWS cloud storage
- AWS Snow Family: physical devices for moving large amounts of data into/out of AWS when network transfer is impractical
  - Snowcone: smallest, portable (up to 14 TB)
  - Snowball Edge: larger (up to 80 TB), can run compute at edge locations
  - Snowmobile: exabyte-scale data transfer via a shipping container
