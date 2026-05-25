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

-
