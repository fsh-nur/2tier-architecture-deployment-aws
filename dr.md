# What is Disaster Recovery?

- A disaster is an unexpected problem resulting in a slowdown, interruption, or network outage in an IT system.
- Disaster recovery in AWS is the process of using AWS cloud services to protect and recover data and applications from disruptions in on-premises or cloud-based environments. 
- AWS Elastic Disaster Recovery (AWS DRS) is a service that continuously replicates server-hosted applications and databases from any source into AWS using block-level replication. 
- AWS DRS can be used for ransomware recovery, point-in-time recovery, and failback of a wide range of applications, without requiring specialized skills.
- AWS DRS also enables users to monitor replication, perform non-disruptive drills, and launch instances for recovery using the AWS Management Console.

## Use Cases

- Replication from a primary site to a secondary site
- DR orchestration between primary and secondary sites
- Failover groups that coordinate the failover of a group of virtual machines
- Virtual labs that are created as part of a failover group configuration

## Benefits

- Ensures business continuity
- Enhances system security
- Improves customer retention
- Reduces recovery costs

## Key Elements of a Disaster Recovery Plan

- Internal and external communication
- Recovery timeline: The timeline should address the following two objectives: The recovery time objective (RTO) is a metric that determines the maximum amount of time that passes before you complete disaster recovery. A recovery point objective (RPO) is the maximum amount of time acceptable for data loss after a disaster. 
- Data backups: The disaster recovery plan determines how you back up your data. Options include cloud storage, vendor-supported backups, and internal offsite data backups.
- Testing and optimization: You must test your disaster recovery plan at least once or twice per year

# S3
## Amazon S3 is object storage built to store and retrieve any amount of data from anywhere. S3 is a simple storage service that offers industry leading durability, availability, performance, security, and virtually unlimited scalability at very low costs.

- Amazon S3 provides a simple web service interface that you can use to store and retrieve any amount of data, at any time, from anywhere. Using this service, you can easily build applications that make use of cloud native storage. Since Amazon S3 is highly scalable and you only pay for what you use, you can start small and grow your application as you wish, with no compromise on performance or reliability.

# AWSCLI: AWS Command Line Interface

- AWS Command Line Interface(AWS CLI) is a unified tool using which, you can manage and monitor all your AWS services from a terminal session on your client.
- AWS has made it possible for Linux, MacOS, and Windows users to manage the main AWS services from a local terminal session’s command line.
- So, with a single step installation and minimal configuration, you can start using all of the functionalities provided by the AWS Management Console using the terminal program., such as in linux Shells and the Windows Command line.

# SDK: Software Development Kits

SDKs provide a comprehensive collection of tools that enable software developers to build software applications faster and in a more standardized way. Also known as a devkit, the SDK is a set of software-building tools for a specific platform, including the building blocks, debuggers and, often, a framework or group of code libraries such as a set of routines specific to an operating system (OS).
