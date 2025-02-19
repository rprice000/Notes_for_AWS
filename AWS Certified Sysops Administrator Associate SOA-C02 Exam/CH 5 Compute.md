CH 5 Compute

1. Amazon Machine Image (AMI)
    - The Amazon Machine Image (AMI) is a server image used to create EC2 instances with a predefined configuration.  AMIs are supplied and maintained by AWS, provided by AWS partners in the Marketplace, offered by the community, or created and managed by the customer.
    - An EC2 instance has two types of root device used for storage of the AMI
        + Instance Store
            ++ Storage Capacity: 10 GiB
            ++ Root volume persistence: Ephemeral
            ++ Boot time: Takes longer to boot (<5min)
            ++ Cost: EC2 instance charges plus S3 cost of storing the AMI
            ++ Modification: Cannot be modified
            ++ Stopping instace: Instance cannot be stopped
        + EBS-Backed
            ++ Storage Capacity: 64 TiB
            ++ Root volume persistence: Default is deleted on termination of instance, but volume can persist
            ++ Boot time: Quick Boot (<1min)
            ++ Cost: EC2 instance charges plus EBS volume cost plus cost of storing the AMI snapshot
            ++ Modification: Can change instance type, kernel, RAM disk, and user data while instance is stopped
            ++ Stopping instace: Instance can be stopped
    - There are two ways to launch an EC2 instance
        + From an AMI: Defines the configuration including an AMI. Allows for automation of the instance creation process as well as versioning

2. Amazon EC2
    - Instances can only be in a stopped or hibernate state if they are EBS-backed.  All instances move from a pending state to a running state and finally to a terminate state.  EC2 instances are billed only in a running state.  Rebooting an instance does not change the hardware; it just restarts the operating system
    - Instances only incur charges when in a running state.  There are costs separate from the instance-EBS storage, data transfer, and elastic IP addresses
    - On-Demand is the baseline model where you are billed per second or hour of usage with no commitment.  Used for short-term, spikey, or unpredictable workloads.
    - Spot instances represent the lowest cost for comput with a savings of up to 90% over on-demand pricing.  Ideal choice for stateless and fault-tolerant workloads or workloads that can be paused.  Capacity Rebalancin is a feature that when enable can signal Auto Scaling or Spot Fleet to automatically replace the impacted instance.
    - Savings Plans have a flexible pricing of up to 72% savings on compute.  Can apply to EC2, Fargate, and Lambda.  Requires a commitment of $/hr of usage over a 1 to 3 year period.
        + Compute Savings Plans: Offer up to 66% savings and allow the most flexibility
        + EC2 Savings Plans: More restrictive but up to 72% savings
    - Capacity Reservations can be placed on EC2 instances to reserve capacity in a specified AZ for indefinite span of time.  Requires 1 to 3 year commitment
    - EC2 Advanced Features
        + Request Spot Instances
            ++ Option says if spot is available at the time of launch use Spot; if not full back to On-Demand
        + Domain Join Directory
            ++ Allow you to join the instances to AWS Directory Services. Instances will need to have a role with sufficient permissions
        + IAM Instance Profile
            ++ Option lets you specify the role used by the instances
        + Hostname Type
            ++ Allows user to choose between the resource name, IP name as the name of the host
        + DNS Hostname
            ++ Using DNS name allows the IP address to change without negative impacts
        + Instance Auto Recovery
            ++ If the instance fails system checks, it is automatically moved to new underlying hardware and rebooted
        + Shutdown Behavior
            ++ Setting determines what state the instance moves into from an OS-level shutdown command
        + Stop-hibernate Behavior
            ++ Hibernate saves the contents of RAM to root volume.  Hibernation can only be enabled before the instance is launched
        + Termination
            ++ Prevents the instance from being terminated through the console, CLI, and SDK until the protection is disabled
        + Stop Protection
            ++ Prevents the instance from being stopped
        + Detailed CloudWatch Monitoring
            ++ Basic monitoring captures data at 5-minute intervals.  Detailed captures data at 1-minute intervals
        + Elastic GPU
            ++ Only available on select Windows instance types.  Used to add networ-attached graphics acceleration without upscaling to a GPU instance type
        + Elastic Inference
            ++ Used on EC2 as well as Sagemaker and ECS. Designed to add deep learning to a non-GPU instance type
        + Credit Specification
            ++ Applies to only T2, T3, T3a instance type.  These are burstable instance types, meaning that at normal CPU untlization levels they build up credits that can be used when the instance needs it above the baseline
        + Placement Groups
            ++ Used to spread or consolidate EC2 instances across the underlying hardware within a single AZ
                +++ Cluster: Used to build low-latency, high-throughput workloads such as HPC by placing instances close together within an AZ
                +++ Spread: Groups spread across separate racks with each instance on its own rack
                +++ Partition: Groups are similar to spread placement groups except that instances are grouped together in partitions and the partitions rather than the instances are placed on separate racks
        + EBS-Optimized Instance
            ++ Only available on some instance types and provides dedicated througput between EC2 and EBS attached volumes
        + Tenancy
            ++ Three forms of tenancy
                +++ Shared: Most commonly used
                +++ Dedicated Instance:  Workloads that requires adherence to certain regulatory compliance or licensing requirements.  No other account can place an instance on that host
                +++ Dedicated Host:  The entire physical host is dedicated to your account.  If you stop and start an instance on a dedicated host the instance returns on the same physical hardware
        + Nitro Enclaves
            ++ Are highly secure and fully isolated instance using the Nitro hypervisor.  Enclaves can be connected using secure local socket (vsock).

3. Amazon EC2 Image Builder
    - Amazon EC2 Image Builder is a tool that makes the creation of images easier by automating the creation, building, and deployment of the image.  Works with both AMIs and container images.
    - Using AWS VM Import/Export (VMIE) you can create:
        + Microsoft Hyper-V (VHDX)
        + VMWare vSphere (VMDK)
        + Open Format Virtualization (OFV)
    - A role will be needed to execute the EC2 Image Builder tasks. The role needs to have EC2InstanceProfileForImageBuilder and AmazonSSMManagedInstanceCore
    - There are four main components for Image Builder
        + Build/Test Component
            ++ Can be created before you create the pipeline.  Similar to user data but more powerful.  You can run updates, install and configure software, or any number of common tasks
        + Recipes
            ++ Based image is defined have
                +++ The image type
                +++ The name, version, and description
                +++ The base image
                +++ The instance can be configured with use data as you would launching an EC2 instance normally
                +++ The working directory can be defined for build and test workflows
                +++ Build and test components can be added
        + Infrastructure Configuration
            ++ Defines things like the instance type, VPC, subnet, security groups, key pairs, the role to use for the instance
        + Distribution Configuration
            ++ Settings here relate to where the image can be distributed including distribution to target regions and accounts
        + Pipeline
            ++ A pipeline is the combination of the elements listed above. Building a pipeline involves 4 steps
                +++ Specify the pipeline details including name/description, the build schedule, and tags
                +++ Define base image
                +++ Define infrastructure
                +++ Define distribution

4. Compute Optimizer
    - Provides recommendations for EC2 instances, Auto Scaling Groups, EBS volumes, and Lambda functions
    - Two versions of Compute Optimizer
        + Default version: Provides recommendation based on CloudWatch Metrics for past 14 days. Free Feature
        + Paid Version: Provides recommendations for past 3 months. Also collects enhanced metrics
    - Will deliver up to 3 recommendations per resource
    - Identify potential resource performance risks or constraints

5. Elastic Load Balancing
    - AWS load balancers come in 3 key forms:
        + Network Load Balancers
            ++ Operate at the Layer 4 and is optimized to move packets of data quickly and efficiently at millions of request per second
            ++ Consists of the load balancer in a public subnet, listeners monitoring ports and protocols, target groups, optional health checks on the targets
            ++ Targets can be EC2 instance ID, IP addresses, or an application load balancer
            ++ Designed to balance loads across two or more AZs
            ++ Integrates with: AWS Config, Traffic Monitoring, and AWS PrivateLink
        + Gateway Load Balancers
            ++ Designed for load balancing third-party virtual appliances using GENEVE (RFC8926)
            ++ Operates at layers 3 and 4 functions as a gateway at layer 3 and a load balancer at layer 4
            ++ Deployed in the same VPC as the virtual appliance but in different subnets
        + Application Load Balancer
            ++ Designed to listen to traffic at Layer 7
            ++ Will listen on any assigned port for HTTP/HTTPS traffic and forward that to a designated target group
            ++ Up to 100 rules can be created for each ALB
            ++ Integrates with:
                +++ AWS Config: Used to monitor configuration changes
                +++ Global Accelerator: Speeds up API workloads by as much as 60% by managing routing
                +++ AWS WAF: Used to provide web traffic filtering to protect your applications from common tasks

6. Auto Scaling
    - Auto Scaling is designed to dynamically add or remove resources and can even predict scaling based on patterns
    - Resource Available for Scaling
        + Aurora
        + EC2
        + ECS
        + DynamoDB
        + Spot Fleets
    - Relies on CloudWatch to monitor metrics of resources.  CloudWatch then signals elastic load balancers to add or remove resources
    - Scaling defines 3 key metrics:
        + Desired capacity: the initial capacity of a group at the time of launch. Auto Scaling attempts to maintain until directed otherwise
        + Minimum Capacity: Lowest capacity a group can scale to. Represents the minimum needed to maintain availability
        + Maximum Capacity: Upper limit to which the group can scale often determined by cost
    - Optimization is always a compromise between optimized for availability or optimized for cost
    - Three tpes of Scaling Options
        + Manual: group is manually scaled
        + Dynamic: Scaling increases or decreases based on triggers.  Triggers typically are CloudWatch metrics
            ++ Target Tracking is a form of dynamic scaling that will maintain a workload at a specified target metric
            ++ Simple Scaling: dynamic scaling based on a single scaling adjustment
        + Predective Scaling: Useful when you have cyclic patterns in utilizations such as high demand during business hours.  Used to have capacity available before demand appears
    - Since auto scaling launches resources, its possible to exceed available quotas.  Service quotas are also known at limits
    - To create copies of instances an auto scaling group needs an original template that will launch the configuration
    - Auto Scaling Groups are used to logical group EC2 On-Demand or Spot Instances for scaling
        + To create an ASG you need:
            ++ Define the group name and launch template
            ++ Select VPC and subnet
            ++ Attach to a load balancer
            ++ Set desired, minimum, and maximum
            ++ Set SNS notifications
            ++ Add tags

7. AWS Application Auto Scaling
    - Supported scalable resources include
        + AppStream 2.0
        + Aurora Replicas
        + Amazon EMR clusters
        + Amazon Neptun clusters
        + Spot Fleet requests
    - There are 3 forms of auto scaling
        + Scheduled Scaling: Used when you have predictable patterns
        + Target Tracking: Used based on CloudWatch metric and a target value for that metric
            ++ Target tracking policy can have one of three effects
                +++ It can change capacity up or down by a specified number
                +++ It can change to a specific value
                +++ It can scale up or down as a percentage
        + Step Scaling: Used to decrease or increase capacity by a specified amount
            ++ Three types of Step Scaling
                +++ ChangeInCapacity: changes the capacity by a specified defined value
                +++ ExactCapcity: changes to a specified defined value
                +++ PercentChangeInCapacity: changes the capcity by a percentage of the existing capacity
    - Auto Scaling is enabled in the console of each resource

8. Lambda
    - Lambda is a completely managed serverless compute service.  Provides a compute resource that runs arbitrary application code in a number of programming languages without the overhead of an OS
    - Three limits to be aware of are the runtime, memory, and concurrency.  Lambda functions have a maximum runtime of 15 minutes and can use a maximum of 10,240 MB of memory, and a soft concurrency quota of 1,000 instances per minute
    - Key Lambda metrics are invocations, durrations, errors, throttles, dead leatter errors, iterator, concurrent executions, and unreserved concurrent executions
    - Lambda functions are often loosely coupled with other services and other Lambda functions to create a solution.