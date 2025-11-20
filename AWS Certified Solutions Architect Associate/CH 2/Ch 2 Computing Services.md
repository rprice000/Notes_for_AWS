Exam Essentials

1. Understand how to provision and launch an EC2 Instance
    - EC2 Amazon Machine Images
      - An AMI is really just a template document that contains informaion telling EC2 what OS and application software to include on the root data volume of the instance it's about to launch.
      - A particular AMI will be available in only a single region although there will often be images with identical functionality in all regions.
      - There are four kinds of AMIs:
        - Amazon Quick Start AMI:  The Quick Start tab on the Launch instance page displays AMIs that are popular choices and that include various releases of Linux or Windows Server Oss and even macOS as well as some specialty images for performing common operations
        - AWS Marketplace AMIs:  AMIs from the AWS Marketplace are official, production-ready images provided and supported by industry vendors
        - Community AMIs:  More than 500 images are available as community AMIs.  Many of these images are AMIs created and maintained by independent vendors and are usually built to meet a specific need.
        - Private AMIs: You can also store images created from your own instance deployments as private AMIs
    - Instance Types
      - AWS allocates hardware resources to your instance according to the instance type or hardware profile you select.
      - 5 Instance Family Types
        - General Pupose:
          - Aims to provide a balance of compute, memory, and network resources
          - Types: Mac, T4g, T3, T2, M6g, M6i, M6a, M5, M5a, M5n, M5zn, M4, A1
        - Compute Optimized:
          - Used for more demanding web servers and high-end machine learning workloads
          - Types:  C7g, C6g, C6i, C6a, Hpc6a, C5, C5a, C5n, C4
        - Memory Optimized:
          - Works well for intensive database, data analysis, and caching operations
          - Types: R6g, R6i, R5, R5a, R5b, R5n, R4, X2gd, X2idn, X2iedn, X2iezn, X1e, X1, High Memory, z1d
        - Accelerated Computing:
          - These instances make use of various generations of high end NVIDIA GPUs.  Recommended for demanding workloads such as high-performance computing and high end financial, engineering, artificial intelligence workloads, and medical research.
          - P4, P3, P2, DL1, Trn1, Inf1, G5, G5g, G4dn, G4ad, G3, F1, VT1
        - Storage Optimized:
          - Delivers fast read/write and come with low-latency access to EBS instance storage volumes.  These instances work well with distributed filesystems and heavyweight data processing applications
    - Instance Behavior
      - You can optionally tell EC2 to execute commands on your instance as it boots by pointing to user data in your instance configuration.  Whether you specify the data during the console configuration process or by using the --user-data value with the AWS CLI, you can have script files bring your instance to any desired state
      - User data can consist of a few simple commands to install a web server and populate its web root, or it can be a sophisticated script setting up the instance as a working node withing a Puppet Enterprise-driven platform
    - Resource Tags
      - The best way to keep a lid on the chaos is to find a way to quickly identify each resource you've got running by its purpose and its relationships to other resources.  The best way to do that is by establishing a consistent naming convention and applying it to tags.  Tags have a key and, optionally an associated value.
    - EBS Volumes
      - You can attach as many EBS volumes to your instance as you like and use them just as you would use hard drives, flash drives, or USB drives with your physical server.  The AWS SLA guarantees the reliability of the data you store on its EBS volumes so you dont have to worry about failure.
      - Amazon's EBS Data Lifecycle Manager can be configured to automate the creation, retention, and deletion of your EBS-based snapshots and AMIs.
      - All EBS volumes can be copied by creating a snapshot.  Existing snapshots can be used to generate other volumes that can be shared and/or attached to other instances or converted to images from which AMIs can be made.  You can also generate an AMI image directly from a running instance-attached EBS volume, although to be sure no data is lost, you should ideally shut down the instance first.
      - Depending how you count them, there are currently 8 EBS volume types.  Five using SSD technologies and three using older spinning hard drives.
        - EBS-Provisioned IOPS SSD
          - If you applications will require intense rates of I/O operations, then you should consider provisioned IOPS. There are currently three flavors of provisioned IOPS volumes: 
            - io1, io2, io2 Block Express
        - EBS General-Purpose SSD
          - This class will work for most regular server workloads that deliver low-latency performance 
        - HDD Volumes
          - This class will work best with large data stores where quick access isn't important
        - Instance Volumes
          - Instance store volumes are ephermeral.  Meaning that when the instance shuts down the data is permanently lost.  Instance store volumes are SSDs that are physically attached to the server hosting your instance and are connected via a fast NVMe
          - The use of instance store volumes is included in the price of the instance itself
          - Instance store volumes work especially well for deployment models where instances are launched to fill short-term roles, import data from external sources, and are effectively disposable.
    - Security Groups
        - An EC2 security group plays the role of a firewall.  By default a secuirty group will deny all incoming traffic while permitting all outgoing traffic. You define group behavior by setting policy rules that will either blok or allow specifed traffic types.  Traffic is assessed by examining its source and destination, the network port it's targeting and the protocol it's set to use.

2. Understand how to choose the right hardware/software profile for your workload
   - Besides the normal charges for running an EC2 instance, your AWS account might also be billed hourly amounts or license fees for the use of the AMI software itself.  Although vendors make every effort to clearly display the charges for their AMIs, it's your responsiblity to accept and honor those charges.
   - EC2 Amazon Machine Images
      - An AMI is really just a template document that contains informaion telling EC2 what OS and application software to include on the root data volume of the instance it's about to launch.
      - A particular AMI will be available in only a single region although there will often be images with identical functionality in all regions.
      - There are four kinds of AMIs:
        - Amazon Quick Start AMI:  The Quick Start tab on the Launch instance page displays AMIs that are popular choices and that include various releases of Linux or Windows Server Oss and even macOS as well as some specialty images for performing common operations
        - AWS Marketplace AMIs:  AMIs from the AWS Marketplace are official, production-ready images provided and supported by industry vendors
        - Community AMIs:  More than 500 images are available as community AMIs.  Many of these images are AMIs created and maintained by independent vendors and are usually built to meet a specific need.
        - Private AMIs: You can also store images created from your own instance deployments as private AMIs

3. Understand EC2 pricing models and how to choose one to fit your needs
   - You can purchase the use of EC2 instances through one of three models
     - On Demand Model
       - Deployments that you expect to run for less than 12 months.
       - This is the most flexible but most expensive on a per-hour basis
     - Reserved Instances
       - If you are planning to run 24/7 for more than a year reserved instances are the best choice.
         - You can pay
           - All up front
           - Partial Up Front
           - No Up Front
         - Terms
           - 1 year
           - 3 years

4. Understand how to configure a security group to balance access with security to match your deployment profile
   - Security Groups
        - An EC2 security group plays the role of a firewall.  By default a secuirty group will deny all incoming traffic while permitting all outgoing traffic. You define group behavior by setting policy rules that will either blok or allow specifed traffic types.  Traffic is assessed by examining its source and destination, the network port it's targeting and the protocol it's set to use.


5. Know how to access a running instance
   - All instances are assigned at least one private IPv4 address that, by default, will fall within one of three blocks
     - From: 10.0.0.0    To: 10.255.255.255
     - From: 172.16.0.0   To: 172.31.255.255
     - From: 192.168.0.0   To: 192.168.255.255
   - Out of the box, you'll only be able to connect to your instance from within its subnet, and the instance will have no direct connection to the Internet
   - You can create and then attach one or more virtual elastic network interfaces to your instance.  Each of these interfaces must be connected to an existing subnet and security group.  You can optionally assign a static IP address within the subnet range
   - An instance can also be assigned a public IP through which full Internet access is possible

6. Be able to describe the features and behavior of storage volume types
   - EBS Volumes
      - You can attach as many EBS volumes to your instance as you like and use them just as you would use hard drives, flash drives, or USB drives with your physical server.  The AWS SLA guarantees the reliability of the data you store on its EBS volumes so you dont have to worry about failure.
      - Amazon's EBS Data Lifecycle Manager can be configured to automate the creation, retention, and deletion of your EBS-based snapshots and AMIs.
      - All EBS volumes can be copied by creating a snapshot.  Existing snapshots can be used to generate other volumes that can be shared and/or attached to other instances or converted to images from which AMIs can be made.  You can also generate an AMI image directly from a running instance-attached EBS volume, although to be sure no data is lost, you should ideally shut down the instance first.
      - Depending how you count them, there are currently 8 EBS volume types.  Five using SSD technologies and three using older spinning hard drives.
        - EBS-Provisioned IOPS SSD
          - If you applications will require intense rates of I/O operations, then you should consider provisioned IOPS. There are currently three flavors of provisioned IOPS volumes: 
            - io1, io2, io2 Block Express
        - EBS General-Purpose SSD
          - This class will work for most regular server workloads that deliver low-latency performance 
        - HDD Volumes
          - This class will work best with large data stores where quick access isn't important
        - Instance Volumes
          - Instance store volumes are ephermeral.  Meaning that when the instance shuts down the data is permanently lost.  Instance store volumes are SSDs that are physically attached to the server hosting your instance and are connected via a fast NVMe
          - The use of instance store volumes is included in the price of the instance itself
          - Instance store volumes work especially well for deployment models where instances are launched to fill short-term roles, import data from external sources, and are effectively disposable.

7. Know how to create a snapshot from a storage volume and how to attach the snapshot to a different instance
   - All EBS volumes can be copied by creating a snapshot. Existing snapshots can be used to generate other volumes tha can be shared and/or attached to other instances or converted to images from which AMIs can be made.  You can also generate an AMI image directly from running instance-attached EBS volume although, to be sure no data is lost, you should ideally shut down the instance first.
   
8. Be able to configure EC2 Auto Scaling 
   - Auto Scaling works by provisioning and starting on your behalf a specified number of EC2 instances.  EC2 Auto Scaling uses either a Launch Configuration or a Launch Template to automatically configure the instances that it launches
   - Launch Configurations
     - Is essentially a named document that contains the same information you'd provide when manually provisioning an instance.
     - They are used only with EC2 Auto Scaling, meaning you can't manually launch an instance using a launch configuration.  Also, once you create a launch configuration you can not modify it.  If you want to change any of the settings, you have to create an entirely new launch configuration.
   - Launch Templates
     - These are essentailly the same as Launch Configurations except you can use them to spin up one-off EC2 instances or even creating a spot fleet.
     - Launch templates are also versioned, allowing you to change them after creation.
   - When you create an Auto Scaling group, it will strive to maintain the minimum number of instances, or the desired number if specified.  If an instance becomes unhealthy, it will terminate and replace it.  Although these checks can catc a variety of instance and host-related problems, they won't necessarily catch application-specific problems.
   - You must specify the minimum and maximum size. You may also optinally set the desired number of instances you want Auto Scaling to provision and maintain.
     - Minimum: Auto Scaling will ensure the number of healthy instances never goes below this number
     - Maximum: Auto Scaling will make sure the number of healthy instances never exceeds this amount
     - Desired Capacity:  The desired capacity is an optional setting that must lie within the minimum and maximum values.  If you dont specify a desired capacity, Auto Scaling will launch the number of instances as the minimum value.
   - Maintaining the current number of instances is just one option.  Auto Scaling provides several other options to scale out the number of instances to meet demand
     - Manual Scaling
       - If you change the minimum, desired, and maximum values at any time after creating the group, Auto Scaling will immediately adjust
     - Dynamic Scaling Policies
       - Dynamic Scaling policies automatically provision more instances before they hit that point.  Auto Scaling generates the following aggregate metrics for all instances within the group
         - Average CPU utilization
         - Average request count per target
         - Average network bytes in
         - Average network bytes out
       - You are not limited to using just these native metrics. You can also use metric filters to extract metrics from CloudWatch logs and use those.
     - Simple Scaling Policies
       - Whenever