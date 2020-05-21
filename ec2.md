## EC2 (Elastic Cloud Compute)

EC2 is Virtual computing environments, known as instances
Preconfigured templates for your instances, known as Amazon Machine Images (AMIs), that package the bits you need for your server (including the operating system and additional software) with various configurations of CPU, memory, storage, and networking capacity for your instances, known as instance types

### Types of EC2
1. On Demand - Spin up ec2 instance when needed.
2. Spot - bid on an instance and it will start with the bid price and when price go higher than bidding price it will shut down. (Only when your compute is flexible)
Note: If you stop your spot instance then you pay for an hr and if AWS stops it then that hr is free
3. Reserved - reserved is cheaper than on demand as it will have contract on these instances (linked to Instance Types)
4. Dedicated Hosts - complete host is dedicated for your EC2 instances. Dedicated Hosts can save you money by enabling you to leverage your existing server-bound software license investments.  Dedicated Hosts also give you more flexibility, visibility, and control over the placement of instances on dedicated hardware. This makes it easier to ensure you deploy your instances in a way that meets your compliance and regulatory requirement

### AMI
1. Choose AMI

![Choose AMI](images/choose-ami.png)


### EC2 Instance Types
2. Choose Instance Type

| __Type__ | __Family__  |
|----------|-------------|
| General Purpose | A T M |
| Compute Optimized | C |
| Memory Optimized | R X Z |
| Accelerated Computing | P G F |
| Storage Optimized | I D H |

__CPU Credits__

AWS EC2 has 2 different type of instances: Fixed Performance Instances(e.g. M3, C3 etc) and Burstable Performance Instances (e.g. T2). Fixed Performance Instances provides a consistent CPU performance whereas Burstable Performance Instances provide a baseline CPU performance under normal workload. But when the workload increases Burstable Performance Instances have the ability to burst, i.e. increase the CPU performance.

CPU Credit regulates the amount CPU burst of an instance. You can spend this CPU Credit to increase the CPU performance during the Burst period. Suppose you are operating the instance at 100% of CPU performance for 5 minutes, you will spend 5(i.e. 5*1.0) CPU Credit. Similarly if you run an instance at 50% CPU performance for 5 minutes you will spend 2.5(i.e. 5*0.5) CPU Credits.
CPU Credit Balance is simply the amount of CPU Credit available in your account at any moment.

When you create an instance you will get an initial CPU Credit. In every hour you will get certain amount of CPU credits automatically(this amount depends on the type of instance). If you don't burst the CPU performance the CPU Credit will be added to your CPU Credit Balance of your account. If you are out of CPU Credit(i.e. CPU Credit Balance turns into 0) your instance will work on baseline performance.

3. Configure Instance

![Configure Instance](images/configure-instance.png)

### EBS (Elastic Block Storage)
4. Add Storage

![Add Storage](images/add-storage.png)

Durability and Backup
* Automatic replication in AZ
* Snapshot backup to S3

I/O Provisioning
* Provision specific level of IOPS
* Or Burstable level of IOPS

#### Volume Types

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

### Storage Types

![Storage Types](images/storage-types.png)

## EBS volumes and snapshots

![Create Snapshot](images/create-snapshot.png)
![Create Volume](images/create-volume.png)

### Security Groups
5. Configure Security Groups

![Configure Security Groups](images/configure-sg.png)

### ENI (Elastic Network Interface)

Elastic Network Interfaces (ENIs) are virtual network interfaces that can be attached to the instances running in an VPC only

ENI consists of the following
- A primary private IP address.
- One or more secondary private IP addresses
- One Elastic IP address per private IP address.
- One public IP address, which can be auto-assigned to the elastic network interface for eth0 when an instance is launched, but only when elastic network interface for eth0 is created instead of using an existing network interface.
- One or more security groups. __Note: SG are attached to ENI not to instance itself__
-  MAC address.
- A source/destination check flag. Disabling this attribute enables an instance to handle network traffic that isn't specifically destined for the instance. For example, instances running services such as network address translation, routing, or a firewall should set this value to disabled. The default value is enabled.
A description

## ELB (Elastic Load Balancing)

Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, and IP addresses.

There are three types of Elastic Load Balancer (ELB) on AWS:
- Classic Load Balancer (CLB) – this is the oldest of the three and provides basic load balancing at both layer 4 and layer 7.
- Application Load Balancer (ALB) – layer 7 load balancer that routes connections based on the content of the request.
- Network Load Balancer (NLB) – layer 4 load balancer that routes connections based on IP protocol data.

![Load Balancers Types](images/load-balancers.png)

- An ELB can distribute incoming traffic across your Amazon EC2 instances in a single Availability Zone or multiple Availability Zones. Only 1 subnet per AZ can be enabled for each ELB.
- Route 53 can be used for region load balancing with ELB instances configured in each region.
- ELBs can be Internet facing or internal-only.


## ASG (Auto Scaling Group)

- Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.
- You create collections of EC2 instances, called Auto Scaling groups.
- Automatically provides horizontal scaling (scale-out) for your instances. Triggered by an event of scaling action to either launch or terminate instances.
- Auto Scaling can span multiple AZs within the same AWS region.

#### Scaling

Scaling Policy
![Scaling Policy](images/scaling-policy.png)

- Can also scale based on an Amazon Simple Queue Service (SQS) queue. Can base off the SQS Metric “ApproximateNumberOfMessages”.
- Cooldown Period: The cooldown period is a configurable setting for your Auto Scaling group that helps to ensure that it doesn’t launch or terminate additional instances before the previous scaling activity takes effect. The default value is 300 seconds.
