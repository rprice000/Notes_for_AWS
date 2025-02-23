CH 6 Storage, Migration, and Transfer

1. Understand how Amazon FSx uses multiple availability zones
    - Amazon FSx is a fully managed service where AWS handles the hardware provisioning, patching, and backups of the underlying architecture used to deliver the high performance and scalable filesystem in AWS
    - Works with several compute options
        + EC2
        + ECS
        + EKS
    - Four options of FSx
        + FSx for NetApp ONTAP 
        + FSx for OpenZFS
        + FSx for Windows File Server
        + FSx for Lustre
    - FSx is highly available and replicates data within or across AZs to protect against failures and increase fault tolerance.  FSx offers replication across regions and integration with AWS Backup.  Has the ability to encrypt data at rest and in transit automatically using KMS. You can run FSx filesystems with access from on premises systems for hybrid-enabled approach to stroage.
    - This is a managed service all replication happens automatically
    - AWS also monitors and maintains the underlying infrastructure components and replaces the failed components or swaps to standby systems in the event of failure

2. Understand how to use AWS DataSync in migrations
    - AWS DataSync assists in automating and accelerating copies of substantial amounts of data between on-premises storage systems and AWS Storage services using common filesystem protocols to copy data between on-premises and AWS Cloud Storage
    - You can use DataSync to create an initial dataset copy or allow scheduled incremental transfers of any data that changed to keep op-premises and cloud dat the same
    - You can configure ongoing data transfers from on-premises systems into AWS for disaster recovery or additional processing
    - Used in populating data lakes running on AWS

3. Understand how to implement AWS Backup for cloud-native backup management
    - AWS Backup allows an organization to centralize and automate data protection across AWS services, including on-premises workloads
    - It integrates with Organizations to manage and deploy data protection policies to govern backup activity across all AWS accounts
    - Protection policies are known as backup plans that define backup frequency and backup retention periods
    - You will assign data protection plans to support resources where Backup will automate the backup process
    - Another key benefit is that Backup can apply data protection policies to create backups of Storage Gateway Volumnes and VMWare virtual machines on-premises.
    - Two primary use cases
        + Cloud-native Backup Solution
            ++ Increases the ability to automate backup activities and incerases the overall resiliency of data stored in AWS.  You have control over the frequency and retention period of the backup plan

4. Understand how to implement Amazon DataLifecycle Manager
    - Datalife cycle Manager allows an organiztion to automate the creation, retention, and deletion of EBS snapshots and EBS-backed AMIs.  It enables cross-account snapshot copy automation and life cycles to reduce storage costs, enforce regular backups schedules, and help create disaster recovery backups and policies across isolated AWS accounts.  There is no additional cost to use Data Life cycle Manager, but you are responsible for the cost of any stored AMI or EBS volume snapshots created by the tool
    - Snapshots are the primary means to back up the data from the EBS volumes.  Successive snapshots are incremental and only contain the volume data changed since the previous snapshots
    - Target resource tags help identify which resources to back up and are customizable to fit the needs of an organization's backup and restoration strategy.  Data Lifecycle Manager tags apply to all snapshots and AMIs created by a policy to provide distinguishing characteristics from snapshots or AMIs created by other means
    - Uses Lifecycle policies and policy schedules to handle the automation tasks used to backup EBS volumes and EBS-backed AMIs
    - Lifecycle Policies consist of core settings
        + Policy Type
        + Resource Type
        + Target Tags
        + Policy Schedules
    - Datalife cycle Manager supports
        + Snapshot Lifecycle policies
        + EBS-backed AMI Life cycle policies
        + Cross account copy event policies
    - Policy schedules enable you to define creation of snapshots or AMIs and how long to retain them

5. Understand use cases for enabling Amazon S3 Cross Region Replication
    - S3 Replication offers the ability to configure S3 to automatically replicate S3 object across different AWS regions using S3 Cross-Region Replication (CRR), or between buckets within the same region using Same-Region Replication (SRR)
    - Supports the use of two way replication between two or more buckets enabling further options when designing a redundant backup strategy
    - Use cases
        + Need for data redundancy
        + When you need to share data across accounts, or the organization has compliance requirements
        + Need to maintain object copies under a different account
    - With CRR you can configure replication at the bucket to grab the entire mapping dataset, or you can change object level using S3 object tags or prefix level if you need to more granularity replicate fies into the backup location
    - Use SRR typically when aggregating logs, such as security or application logs, into a single bucket
    - When configuring replication, any new objects placed in the buckets automatically replicate to the destination
    - Any existing objects in the bucket after configuring replication would not copy to the replication destination.  To address this issue, you can use S3 Batch Replication to backfill newly created replication buckets with objects from existing buckets

6. Understand how to implement Amazon S3 Lifecycle Rules
    - This feature allows you to configure a set of rules that allow you to define actions that S3 applies to a group of objects
    - Two different types of action types
        + Transition actions: assist in moving objects between storage classes
        + Expiration actions: assist in deletion of objects on your behalf
    - This feature's rules can use tags or prefixes to determine which objects or subset of objects in the bucket have the Lifecycle rule applied
    - Using a Lifecycle you can configure time durations, object sizes, or other object or bucket conditions to move files between storage tiers

7. Understand use cases for Amazon S3 Glacier storage classes
    - To address long-term storage needs and provide the lowest cost per GB storage option, S3 Glacier
    - Glacier S3 has 3 storage options
        + Amazon S3 Glacier Instant Retrieval
        + Amazon S3 Glacier Flexible Retrieval
        + Amazon S3 Glacier Deep Archive
    - S3 Glacier Instant Retrieval
        + Primary usage is data that rarely requires access such as once or twice a quarter and when accessing the data, you require the data to be available within milliseconds
        + There is a minimum storage duration of 90 days for objects
    - S3 Glacier Flexible Retrieval
        + Ideal use case is for data that will be accessed once or twice during an entire year and that restores asynchronosly
        + Retrieval can be ansynchronous and does not require millisecond retrieval times
        + When restoring you will initiate a retrieval request, which creates a temporary copy of the data requested in an S3 Standard storage class.  Leaving the archived data intact and untouched
        + S3 Event Notification is used to know when an object is successfully restored and the temporary copy is ready for use within the temporary S3 Bucket
        + Three types of Retrieval options
            ++ Expediated: Data available in 1 to 5 minutes
            ++ Standard: Data available in 3 to 5 hours
            ++ Bulk: Data available in 5 to 12 hours
    - S3 Glacier Deep Archive
        + Provides long-term data storage, the type of data access once or twice every few years
        + Significantly lower cost than maintaining the storage or magnetic tape libraries on-premises
        + Used to reduce or discontinue the use of on-premises magnetic tape libraries
        + Two types of Retrieval
            ++ Standard: Data available within 12 hours
            ++ Bulk: Data available within 48 hours
        + Can use AWS Storage Gateway with Tape Gateway feature to store data on tapes directly into Glacier Deep Archive

8. Understand how to configure Amazon S3 static web hosting
    - Enables organiztions to scale short-term or in some caes long-term website solutions using the abilities of S3
    - You can enhance support for increased traffic by implementing CloudFront to cache frequently accessed files
    - This allows for solutions to minimize cost, utilize the elasticity, durability, and availability of the S3 service
    - Static web hosting means web content that does not require server side lanaguage and technology to build or display content
    - Static content loads faster, more secure, and is easier to design as it uses HTML
    - Helps with disaster recovery by being a location to display a simple web page as part of a failover activity when the primary web server is down

9. Understand how to monitor Amazon EBS volume performance
    - There are a few factors that can impact performace of an EBS volume
        + Ensure that the EC2 instance type supports that use of EBS optimization
            ++ This prevents EBS volume tarffic from contending with your instance's network traffic
        + Understand the worload that is accessing the EBS volume and ensuring that you select the proper volume
    - You can use CloudWatch when evaluating the EBS volumes
        + List of important CloudWatch metrics
            ++ VolumeQueueLength
            ++ VolumeReadBytes
            ++ VolumeWriteBytes
            ++ VolumeReadOps

10. Understand how to implement S3 performace features
    - S3 has two performace features regarding data migration
        + Amazon S3 Transfer Acceleration
            ++ Used as a method to increase and optimize transfer speeds from across the world into S3 buckets
            ++ It uses the Amazon CloudFront edge locations network as an upload point to reduce latency and increase traffic speed
            ++ The destination S3 Bucket must be DNS-compliant and not contain any periods, transfer acceleration must be enabled on the bucket, and you must be aware that Transfer Accleration only supports virtual-hosted style requests when using REST API calls
            ++ It is important to not that unless the bucket owner has delegated permission to get the accleration state on the S3 bucket, the bucket owner is the only user that can enable this state
            ++ You can use the S3 Transfer Accelerator Speed Comparison tool when determining if Amazon S3 Transfer Acceleration is going to improve performance for you applicaiton or use case
        + Amazon S3 Multipart Uploads
            ++ Helps with pausing and resuming object upload
            ++ Has the ability to recover from network issues
            ++ Three step process
                +++ Initiate the upload
                +++ Upload the object parts
                +++ Complete the multiplart upload once all part uploads are complete
            ++ Each upload will have various unique identifiers that are either produced or that you select during the process
            ++ You must include the upload ID whenever you upload parts, list the parts, or complete or stop the upload
            ++ S3 will return an entitiy tag (ETag) header in the response for each part upload
            ++ For S3 to consider a multipart upload complete you must complete the multipart upload by including the unique upload ID and a list of both part numbers and corresponding ETag values.