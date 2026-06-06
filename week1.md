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

Cloud Formation

- supports infrastructure as code (IaC), enabling consistent, repeateable deployments across different environments
- designed to handle complex setups.
- defines infrastructure as code to help make sure that deployments are consistent across different environments such as development, testing, and production.
- With CloudFormation, users can model and set up their AWS resources using code to automate provisioning and the management of infrastructure
  - This method can help to reduce errors and maintain consistency across environments.

# Module 5: Networking

Amazon Virtual Private Cloud (VPC)

- logically isolated section of the AWS Cloud — your own private network
- can be public(accessibly to internet) or private
- you define the IP address range, subnets, route tables, and gateways
- resources inside a VPC are not accessible from the internet by default

Subnets

- a section of a VPC that groups resources based on security or operational needs
- control traffic permissions
  - Network Access Control List (Network ACL)
    - stateless
    - every package that crosses the subnet boundaries get checked against
    - check if package has access to either enter/leave subnets
    - does not check if package can reach specific instances
  - security group
    - stateful (has some kind of memory: who to allow/who not to)
    - block all traffic trying to access instances unless specified
- Public subnet
  - has a route to an Internet Gateway → resources can communicate with the internet
  - e.g. web servers, load balancers
- Private subnet
  - no direct internet access
  - e.g. databases, internal application servers
- inter-subnet communication
  - you can define rules within a VPC to allow resources in different subnets to communicate
  - e.g. EC2 instances in a public subnet communicating with databases in a private subnet

Gateways and Connections

- Internet Gateway (IGW)
  - attaches to a VPC to allow traffic between the VPC and the internet
  - required for resources in public subnets to be reachable
  - doorway open to public
- Virtual Private Gateway
  - entry point for encrypted VPN connections from on-premises networks into the VPC
  - traffic still travels over the public internet but is encrypted
- AWS Direct Connect
  - dedicated private physical connection from on-premises data center to AWS
  - not over the public internet → lower latency, more consistent bandwidth
  - good for high-throughput or compliance-sensitive workloads

VPN and Private Connectivity

- AWS Client VPN
  - managed, client-based VPN service that lets individual users (remote workers, employees) securely connect to AWS resources or on-premises networks from any location
  - uses OpenVPN-based protocol; users install a VPN client on their device
  - authentication options: certificate-based, Active Directory, or SAML 2.0 (federated SSO)
  - when to use:
    - remote workforce needs secure access to AWS resources or a corporate network
    - replacing traditional on-premises VPN concentrators
    - BYOD (bring your own device) scenarios where per-user access control is needed

- AWS Site-to-Site VPN
  - creates an encrypted IPSec tunnel between an entire on-premises network and an AWS VPC over the public internet
  - AWS side: Virtual Private Gateway (VGW) or AWS Transit Gateway; on-premises side: Customer Gateway device
  - provides two tunnels automatically for redundancy
  - when to use:
    - connecting an entire office or data center network to AWS (network-to-network, not user-to-network)
    - quick, cost-effective hybrid connectivity when dedicated lines are not needed
    - lower-bandwidth workloads or as an encrypted backup path for AWS Direct Connect

- AWS PrivateLink
  - establishes private connectivity from a VPC to AWS services or your own services without traffic ever traversing the public internet
  - uses Interface VPC Endpoints (ENIs in your subnet) powered by PrivateLink, and Gateway Endpoints for S3 and DynamoDB
  - traffic stays entirely within the AWS network backbone
  - when to use:
    - accessing AWS services (S3, DynamoDB, API Gateway, etc.) from a VPC without a public internet route
    - exposing your own service to other VPCs or AWS accounts privately (avoid VPC peering for service access)
    - SaaS providers exposing services to customers without granting full VPC access
    - compliance requirements that prohibit any public internet traffic

- AWS Direct Connect
  - dedicated private physical fiber connection from your on-premises data center to AWS — does not travel over the public internet
  - available at 1 Gbps, 10 Gbps, and 100 Gbps; lower speeds available via AWS Partner hosted connections
  - provides consistent latency and predictable throughput, unlike internet-based VPNs
  - when to use:
    - high-throughput workloads such as large data transfers, media production, or database replication
    - compliance or regulatory requirements that mandate traffic must not cross the public internet
    - hybrid architectures with sustained, heavy traffic between on-premises and AWS
    - can be combined with Site-to-Site VPN to add encryption over the Direct Connect link

Network Traffic in a VPC

- data moves through a VPC as packets — a unit of data sent over the internet or a network
- incoming request journey: client → public internet → Internet Gateway → NACL check at subnet boundary → subnet → Security Group check → resource (EC2 instance)
- two permission checkpoints before a packet reaches a resource:
  1. Network ACL: at the subnet boundary — checks who sent the packet and how it's trying to communicate
  2. Security Group: at the instance level — final check before the packet reaches the resource

Network Traffic Filtering

- Network Access Control Lists (NACLs)
  - virtual firewall that checks packets crossing the subnet boundary in both directions
  - stateless: remembers nothing — each packet is evaluated against the rules independently, both inbound and outbound, every time
  - rules are evaluated in order (lowest number first)
  - default NACL: allows all inbound and outbound traffic
  - custom NACLs: deny all traffic by default until you add explicit allow rules
  - has an explicit catch-all deny rule: any packet that doesn't match a rule is denied
- Security Groups
  - virtual firewall at the individual resource level (e.g. each EC2 instance)
  - stateful: remembers previous decisions — if a packet was allowed in, the response is automatically allowed out regardless of outbound rules
  - default: deny all inbound, allow all outbound
  - only allow rules — you cannot add explicit deny rules (unmatched traffic is denied by default)
  - multiple EC2 instances within the same VPC can share a security group or have separate ones

| Feature        | NACLs                                  | Security Groups                      |
| -------------- | -------------------------------------- | ------------------------------------ |
| Scope          | Subnet level                           | Instance level                       |
| State          | Stateless                              | Stateful                             |
| Rule types     | Allow and deny rules                   | Allow rules only                     |
| Return traffic | Must be explicitly allowed             | Automatically allowed                |
| Default        | Allow all (default); Deny all (custom) | Deny all inbound, allow all outbound |

Amazon Route 53 (DNS)

- highly available and scalable Domain Name System (DNS) service
- translates domain names (e.g. example.com) into IP addresses
- also handles domain registration
- Routing policies:
  - Simple: route to a single resource
  - Weighted round robin: split traffic across multiple resources by percentage
  - Latency-based: route to the Region with lowest latency for the user
  - Failover: route to a backup resource if the primary is unhealthy
  - Geolocation: route based on user's geographic location

VPN vs AWS Direct connect

- VPN
  - secure, flexible, remote access, small-scale, dedicated connection isnt necessary
- AWS Direct connect
  - High bandwidth, low latency, consistent performance, large data transfer, critical applications
- Both
  - VPN as failover of direct connect

Company that needs to deliver content globally

- Route 53 --> Amazon CloudFront --> respective regions
- route 53 determine which region is closest to user and directs to appropriate cloudfront edge location
- edge location fetches content

# Module 6: Storage

Types of Storage

- Block Storage (ideal for applications that need quick and frequent updates)
  - Data divided into pieces called blocks
  - direct data access without file system layers
  - best for applications/databases needing fast, frequent updates
- object Storage
  - Object = data + unique ID + metadata
  - full rewrite required to update an object
  - organized using buckets
  - best for large or infrequently changed files
- File storage
  - cloud-based access through shared file systems
  - straightforward implementation without code changes
  - best for applications needing shared file access

Amazon Simple Storage Service (S3): Object Storage

- object storage — store any type of data as objects inside buckets
- each object = data + metadata + unique key
- virtually unlimited storage
- maximum single object size is 5 TB
- create multiple objects
- version objects (data back-ups)
- highly durable: data is automatically replicated across multiple AZs
- Amazon S3 Security
  - private access by default
  - bucket policies
  - presigned URLs (temporary access), time limited
  - Amazon S3 access points
  - Amazon S3 audit logs (track every access)
- Storage classes (choose based on access frequency) --> designed for diff storage needs, can have multiple storage classes in a single bucket
  - S3 Standard
    - frequently accessed data; high durability, stored across ≥3 AZs
  - S3 Standard-IA (Infrequent Access)
    - lower storage cost, retrieval fee applies (good for back-up data)
  - S3 One Zone-IA
    - stored in a single AZ; cheaper, but less resilient
  - S3 Glacier Instant Retrieval
    - archive data, millisecond retrieval
  - S3 Glacier Flexible Retrieval
    - archive, retrieval in minutes to hours
  - S3 Glacier Deep Archive
    - lowest cost; retrieval within 12 hours; long-term retention
  - S3 Intelligent-Tiering
    - automatically moves objects between tiers based on access patterns
    - frequent access, infrequent access, archive instant, acess deep archive
- S3 Lifecycle Policies: automation rule to delete/move data we can set up
  - S3 Storage Class Analysis
- Static website hosting: upload HTML, CSS, JS, and media files to a bucket, enable static web hosting → instant website
  - automatically scales to handle any amount of traffic
  - pay only for storage used and data transferred out
  - NOT suitable for databases — not designed for rapid, continuous rewrite operations (use EBS for that)

Amazon Elastic Block Store (EBS): Block Storage

- block storage volumes attached to EC2 instances (like a hard drive for a server)
- data persists independently from the EC2 instance lifecycle
- can only be attached to one EC2 instance at a time (within the same AZ)
- performance measured in Input/output per second (IOPS)
- different volume types exist — choose based on workload:
  - Provisioned IOPS SSD: highest performance, for mission-critical apps like databases
- ideal for relational databases on EC2 — block-level access is essential for database read/write operations
- EBS Snapshots:
  - point-in-time backups stored in S3
  - can be done daily, weekly, monthly etc
  - can do incremental backup --> only copies what has changed
    - makes snapshots faster and more storage efficient
- Amazon Data Lifecycle Manager
  - schedule automatic snapshot creation
  - set retention policies
  - manage snapshot lifecycle
  - apply consistent backup policies

Amazon Elastic File System (EFS)

- managed NFS (Network File System) — shared file storage
- multiple EC2 instances across multiple AZs can read/write simultaneously
- scales automatically (up to petabytes) as files are added or removed — no provisioning needed
- low latency with high aggregate throughput and IOPS
- good for shared content, home directories, CMS workloads, large media files (images, video), real-time multi-location access

EFS vs EBS

- EBS: like a hardrive
  - volumes attach to EC2 instances
  - Availability Zone level resources
  - need to be in the same Availability Zone to attach EC2 instances
  - volume do not automatically scale
- EFS
  - Multiple instances reading and writing simultaneously
  - Linux file system
  - Regional Resource
  - Automatically scales

Amazon FSx

- fully managed, high-performance file systems in the cloud
- supports multiple filesystem protocols (unlike EFS which focus on Network File System only)
- handles hardware provisioning, patching, and backups automatically
- built on latest AWS compute, networking, and disk technologies for high performance and lower TCO

| File System                 | Protocol                 | Best For                                           |
| --------------------------- | ------------------------ | -------------------------------------------------- |
| FSx for Windows File Server | SMB (Windows)            | Windows workloads, SQL Server, virtual desktops    |
| FSx for NetApp ONTAP        | NFS, SMB, iSCSI          | Hybrid workloads, modern apps, business continuity |
| FSx for OpenZFS             | NFS (v3, v4, v4.1, v4.2) | Data analytics, content management, dev/test       |
| FSx for Lustre              | Lustre                   | ML, HPC, big data analytics, media workloads       |

- FSx for Windows File Server use cases:
  - migrate Windows file servers to AWS
  - accelerate hybrid workloads
  - reduce SQL Server deployment cost
  - streamline virtual desktops and streaming
- FSx for NetApp ONTAP use cases:
  - migrate workloads to AWS seamlessly
  - modernize data management
  - streamline business continuity
- FSx for OpenZFS use cases:
  - deliver insights faster for data analytics
  - accelerate content management
  - increase dev/test velocity
- FSx for Lustre use cases:
  - accelerate machine learning (ML)
  - enable high performance computing (HPC)
  - unlock big data analytics
  - increase media workload agility

Additional Storage Services

- AWS Storage Gateway:
  - hybrid storage — connects on-premises environments to AWS cloud storage
  - Good for disaster recovery, data archiving
    - S3 File Gateway
      - appears to local systems as a standard file server using familiar file protocols
      - files written are automatically uploaded to S3; recently used data cached locally for low latency
      - on-premises apps get access to virtually unlimited cloud storage without code changes
    - Volume Gateway: presents cloud data as iSCSI volumes mountable by existing applications
      - Cached volume mode: primary data stored in the cloud, frequently accessed data cached locally
      - Stored volume mode: complete dataset kept locally, asynchronously backed up to AWS as EBS snapshots
    - Tape Gateway
      - replaces physical tape infrastructure with virtual tape backed by S3
      - presents itself to backup software as standard tape hardware — no changes needed to existing backup workflows
      - can automatically transition infrequently accessed tapes to a cheaper storage class for long-term retention
- AWS Snow Family: physical devices for moving large amounts of data into/out of AWS when network transfer is impractical
  - Snowcone: smallest, portable (up to 14 TB)
  - Snowball Edge: larger (up to 80 TB), can run compute at edge locations
  - Snowmobile: exabyte-scale data transfer via a shipping container

Elastic Disaster Recovery

- continuously replicates servers' block-level data to AWS for rapid recovery during disruptions
- supports both physical and virtual servers
- minimises downtime and data loss without the cost of maintaining a secondary data center
- non-disruptive disaster recovery testing — can launch recovery instances at any time to validate procedures
- Benefits:
  - business resilience
  - streamlined disaster recovery
  - cost optimisation (eliminates secondary data center)
- Use cases:
  - Healthcare: replicate on-premises servers to AWS to protect patient records and meet compliance requirements
  - Financial services: continuously replicate transaction processing systems so a bank can quickly recover if its primary data center fails
  - Manufacturing: replicate factory management servers to protect production planning and minimise supply chain disruption

# Module 7: Databases

Amazon Relational Database Service (RDS)

- automated patching, backups, redundancy, failover, and disaster recovery
- fully managed relational database service
- Querying relational data
  - MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Amazon Aurora
- Multi-AZ deployment
  - automatic standby replica in another AZ for high availability

Amazon Aurora

- managed relational database designed to help reduce unnecessary I/O operations.
- offers up to five times the throughput of standard MySQL while maintaining compatibility
- PostgreSQL, MySQL, DSQL
- up to 15 Aurora Replicas across AZs
- AWS backup support
- up to 5× faster than standard MySQL, 3× faster than PostgreSQL
- storage auto-scales up to 128 TB
- good choice when you need high performance and AWS-native integration

Amazon DynamoDB (non-relational)

- data = items = set of attributes
- attribute = name + value
- add/remove attributes at any time
- fully managed, serverless NoSQL key-value and document database
  - stored in non-relational
  - no schema — flexible data structure per item
- single-digit millisecond response times at any scale
- automatically scales throughput up and down based on demand
- good for high-traffic web apps, gaming leaderboards, IoT data
- DynamoDB Global Tables
  - e.g. Amazon prime day
  - tens of trillions of calls
  - 146 million requests/second

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

In-Memory Caching Services

- Data caching
  - stored in system memory (cache)
  - near-instantaneous access
  - redis OSS, Valkey, Memcached
- Amazon ElastiCache
  - fully managed in-memory caching service
    automates key management tasks
  - dramatically reduces database load by caching frequently read data in memory
  - supports two engines:
    - Redis: supports persistence, replication, pub/sub, sorted sets — good for leaderboards, sessions, queues
    - Memcached: simple, multi-threaded, pure caching — good for large-scale horizontal scaling
  - sub-millisecond response times
  - use cases: session management, real-time leaderboards, database query caching, rate limiting
  - reduce operational overhead
  - cost-optimization tool for database
- Amazon MemoryDB for Redis
  - durable, Redis-compatible in-memory database (not just a cache)
  - data persists across restarts — data stored in a Multi-AZ transaction log
  - use when you need Redis speed AND durability as the primary database, not just a cache layer

Additional Database Services

- Amazon DocumentDB (MongoDB compatible)
  - handle semistructured data
    - information that doesn't conform to rigid relational schemas
  - fully managed document database
  - stores, queries, and indexes JSON data
  - good for content management, user profiles, catalogs
- Amazon Keyspaces (for Apache Cassandra)
  - managed, serverless Cassandra-compatible database
  - wide-column store; ideal for high-throughput, time-series, and IoT workloads
  - no servers to manage; scales automatically
- Amazon Neptune
  - fully managed GRAPH database
  - optimised for storing and querying highly connected data (nodes and relationships)
  - use cases:
    - social networks, fraud detection, knowledge graphs, recommendation engines
- Amazon Timestream
  - fully managed, serverless time series database
  - purpose-built for data that changes over time (IoT sensor data, application metrics, server logs)
  - automatically scales and moves older data to cheaper storage tiers
- Amazon QLDB (Quantum Ledger Database)
  - fully managed ledger database with an immutable, cryptographically verifiable transaction log
  - every change is recorded permanently — cannot be altered or deleted
  - use cases:
    - financial transactions, supply chain tracking, audit trails, compliance records
- AWS backup
  - streamlines data protection across various AWS resources and on-premises deployments by providing a single dashboard for monitoring and managing backups

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
