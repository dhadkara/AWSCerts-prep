## EC2 (Elastic Cloud Compute)

EC2 is Virtual computing environments, known as instances
Preconfigured templates for your instances, known as Amazon Machine Images (AMIs), that package the bits you need for your server (including the operating system and additional software) with various configurations of CPU, memory, storage, and networking capacity for your instances, known as instance types

### Types of EC2
1. On Demand - Spin up ec2 instance when needed.
2. Spot - bid on an instance and it will start with the bid price and when price go higher than bidding price it will shut down. (Only when your compute is flexible)
Note: If you stop your spot instance then you pay for an hr and if AWS stops it then that hr is free
3. Reserved - reserved is cheaper than on demand as it will have contract on these instances (linked to Instance Types)
4. Dedicated Hosts - complete host is dedicated for your EC2 instances. Dedicated Hosts can save you money by enabling you to leverage your existing server-bound software license investments.  Dedicated Hosts also give you more flexibility, visibility, and control over the placement of instances on dedicated hardware. This makes it easier to ensure you deploy your instances in a way that meets your compliance and regulatory requirement

## ADD MORE DETAILS

## EBS (Elastic Block Storage)

Durability and Backup
* Automatic replication in AZ
* Snapshot backup to S3
I/O Provisioning
* Provision specific level of IOPS
* Or Burstable level of IOPS


### Volume Types

1. SSD-General Purpose-gp2
IOPS upto 10,000 -Moderate workloads frequent access
Bootable
2. SSD-Provisioned IOPS -io1
IOPS upto 20,000 - Sustainable IOPS like large db e.g. Mongodb,Cassandra etc (max 16TiB)
Bootable
3. HDD-Throughput Optimized -st1
Streaming workloads requiring consistent, fast throughput like Big data, Data warehousing, log processing etc.
Not Bootable
4. HDD ,Cold -sc1
Scenarios where the lowest storage cost is important
Not Bootable
5. HDD, Magnetic - Standard (Previous generation)
Bootable



