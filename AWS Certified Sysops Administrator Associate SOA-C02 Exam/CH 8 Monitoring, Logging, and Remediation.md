CH 8 Monitoring, Logging, and Remediation

1. Recognize use cases for which CloudWatch is well suited
    - CloudWatch doesn't provide a direct analog for physical devices and on-premises datacenter activities.  It does provide robust system for managing metrics
    - Almost every single service and resource provides metrics to CloudWatch, CloudWatch becomes a sort of repository for all those collected metrics.  It give you tools too wade through the huge amount of collected data.

2. Recite the core components of a CloudWatch event
    - CloudWatch has three key components
        + Events: An event is the thing that is being reported and is a proxy for that thing happening
        + Rule: A rule is an expression that matches incoming events.  If there is a match to an event, the event is routed to a target for processing
        + Target: A target is typically a piece of code in Lambda or an Auto Scaling group or perhaps an email that should be sent out.

3. Recognize name of CloudWatch metrics
    - Instance Metrics you should be familiar with:
        + CPUUtilization
        + DiskReadOps
        + DiskWriteOps
        + DiskReadBytes
        + DiskWriteBytes
        + NetworkIn
        + NetworkOut
        + NetworkPacketIn
        + NetworkPacketOut
    - EBS Metrics you should be familiar with:
        + EBSReadOps
        + EBSWriteOps
        + EBSReadBytes
        + EBSWriteBytes
        + EBSIOBalance%
        + EBSByteBalance%
        + These metrics are specifically available for the following instance family types: C, M, R, and T3
    - ECS Metrics you should be familiar with:
        + CPUUtilization
        + CPUReservation
        + MemoryReservation
        + MemoryUtilization
    - S3 Metrics you should be familiar with:
        + BucketSizeBytes
        + NumberOfObjects
        + AllRequests
        + GetRequests
        + BytesDownloaded
        + BytesUploaded
        + FirstByteLatency
        + TotalRequestLatency
    - RDS Metrics you should be familiar with:
        + DatabaseConnection
        + DiskQueueDepth
        + FreeStorageSpace
        + ReadIOPS
        + ReadLatency
        + ReplicaLag
    - DynamoDB Metrics you should be familiar with:
        + ConsumedReadCapacityUnits
        + ConsumedWriteCapcityUnits
        + ProvisionedReadCapacityUnits
        + ProvisionedWriteCapacityUnits
        + ReplicationLatency
        + SystemErrors

4. Explain how a CloudWatch alarm works
    - An alarm is intended to go off when a metric is outside of a set of values you consider "okay".  You can set a specific value as a high or low value, or a range of acceptable values
    - You should specify how many periods the metric must be above or below a threshold
    - Once a threshold is set an alarm can be in one of three states
        + OK
        + ALARM
        + INSUFFICIENT_DATA
    - When the alarm initiates an action, you can do something

5. List and Explain the three CloudWatch States
    - OK: If your CloudWatch Alarm is OK, that means that the metric or the mathematical expression behind the metric is within the defined threshold
    - ALARM: If your CloudWatch alarm says it is in an ALARM state, that means that the metric or the mathematical expression behind the metric is below or above the defined threshold
    - INSUFFICIENT_DATA: There are a couple of reasons that your alarm might be in this state. The most common reasons are the alarm has only just started/been created, the metric it is monitoring is not available, or there is simply not enough data at this time to determine whether the alarm should be in an OK or an ALARM state

6. Create custom metrics for anything above the hypervisor
    - CloudWatch functions below the AWS hypervisor, which means that it functions below the virtualization layer of AWS.  This means that if can report on things like CPU usage and disk I/O, but it cannot see what is happening above that layer
    - This means CloudWatch can not tell you what tasks or application processes are affecting performance.  It can only report on the information it can directly see at the hypervisor layer, or things that are reported to it

7. Differentiate between CloudWatch, CloudTrail, and AWS Config
    - CloudWatch
        + A monitoring and observability service that collects metrics, logs, and events from AWS resources and applications
        + It helps set alarms, visualize data, and automate responses to operational changes
        + Use if for performance monitoring, anomaly detection, and operational insights
    - CloudTrail
        + A service that records API calls and user activities across your AWS account
        + It helps with security auditing, compliance, and troubleshooting by tracking who did what, when, and from where
        + You can stage logs in S3, analyze them with Athena, or trigger alerts for suspicious activity
    - AWS Config
        + A service that tracks and evaluates changes to your AWS resources against predefined compliance rules
        + It provides a detailed configuration history, detects drift, and help with governance and compliance reporting
        + Useful for enforcing security policies and understanding resource dependencies

8. Describe the two types of trails:  Cross-Region and Single-Region
    - Cross-Region Trails
        + You specify a trail, and then CloudTrail applies that trails to all regions. The logs still go to an S3 bucket you choose.  Trails apply across all regions by default. All regions tails are ideal because you get a single configuration that is applied across all your regions consistently.  You also get all your logs from all regions in a single S3 bucket.  If you launch resources in a new region, trails that apply to all regions automatically are applied to the new region.  You don't have to do anything to get the trail configuration, which is another benefit
    - Single-Region Trails
        + There's not often a good reason to use this approach typically if you want to log certain activity in one region you will want to log all regions
        + The primary use case would be that you are troubleshooting something very specific
    - In both cases you log output to any S3 bucket, regardless of the region withing which the bucket exists.

10. Describe the best practices for acting on and reviewing CloudTrail Logs
    - Store CloudTrail logs in S3 for long-term retention
    - Stream CloudTrail logs to CloudWatch logs for real-time monitoring
    - Setup CloudWatch alarms for security and anomaly detection
    - Perform advanced log analysis with Athena
    - Automate responses with Lambda and Security Hub
    - Enable AWS Config to track configuration changes

11. Explain the use of AWS Config in monitoring, especially as compared to CloudWatch and CloudTrail
    - AWS Config is primarily used for tracking changes in AWS resource configurations and ensuring they comply with security and operational best practices
    - What this means is AWS Config's primarily focus is  configuration monitoring and compliance while CloudWatch is performance monitoring and alerting, and CloudTrail is security auditing and API tracking
    - Config tracks changes over time with configuration history, CloudWatch does not track changes and only tracks logs and metrics, and CloudTrail tracks API changes
    - Config has compliance monitoring through config rules and autoremediation, but both CloudWatch and CloudTrail have no compliance monitoring
    - Config has limited real-time alerts through rule violations, CloudWatch has real time alerts through alarms and metrics, CloudTrail has limited real time alerts through CloudWatch
    - Config has security monitoring through compliance rules, CloudWatch has limited security monitoring through logs and alarms, and CloudTrail has secuirty monitoring through tracking API activity.

12. List the benefits of AWS Config
    - Continous Resource Monitoring
        + Tracks config changes in real time
        + Provides detailed history of config changes
        + Helps identify unauthorized or unintended changes
    - Compliance and Governance Enforcement
        + Enables compliance and monitoring with Config rules
        + Automatically flags non-compliant resources and provides remediation steps
    - Security and Risk Management
        + Detects misconfigurations and security vulnerabilities
        + Works with Security Hub for centralized security management
    - Automatic Remediation
        + Can automatically fix misconfigured resources
    - Drift Detection and Change Tracking
        + Help audit and rollback changes
        + Detects drift in CloudFormation stacks
        + Maintain a complete change history
    - Integrates with other Services
        + Works with CloudTrail to track API related config changes
        + Sends alerts to CloudWatch when config rules are violated
        + Stores history in S3

13. Explain AWS Config rules and how are they Evaluated
    - A rule in AWS Config is simply a desired configuration for a resource.  It can describe a specific value or a set of values that a property can take
    - A configuration item represents a specific configuration. A rule evaluates a resource's configuration at a given point in time.  The resource itself provides configuration information through configuration items. A configuration item (CI) is an attribute and value (or values) for that attribute, reported against a specific resource
    - When you write a rule, AWS Config evaluates the values reported in configuration item attributes against rules.  If the value doesn't match, then the rule is considered broken and the configuration is reported as noncompliant.  A notification is then sent, and your AWS Config dashboard will report the noncompliant item
    - There are three types of rules
        + AWS managed rules are used as is or customized to suit your needs.  You can create custom Lambda functions and add them to Config.  You associate each custom rule with a Lambda function containing the logic that evaluates whether your resources comply with rules
        + You can create custom rules using CloudFormation Guard.

15. Describe the two ways rule evaluation can be triggered
    - Proactive Evaluation
        + Enabled prior to resource provisioning
    - Detective Evaluation
        + Enabled evaluation of resources that have been provisioned
    - After selecting an evaluation mode you define the trigger type
        + Configuration Change Trigger: Set AWS Config to evaluate rules any time a change on a resource is reported
        + Periodic Triggers: Set AWS Config to evaluate rules on a specific frequency. Set frequency to 1 hour, 3 hours, 6 hours,12 hours, or 24 hours.
    - For Change Triggers specifcially you can st when evaluation occurs
        + All Changes: Triggers when any resource is created, deleted, or changed
        + When a resource matches a specified type
        + When a resource tage matches a specified tag

16. Explain how AWS Systems Manager is able to help with operational tasks
    - AWS Systems Manager (SSM) is free service offered by AWS that provides patching automation, software inventory, and software installation and configuration.  It allows you to group systems logically, and it integrates with both AWS Config and CloudWatch.  It can monitor both Windows and Linux OS by utilizing the SSM agent.

17. Explain the use of the various components of AWS Systems Manager
    - Run Command
        + Uses command documents to execute actions against one or more managed EC2 Instances
    - Patch Manager
        + Allows you to patch whole fleets of EC2 instances and on-premises systems automatically
        + Using maintenance tasks, you can schedule patch installation to install only approved patches
        + Uses Patch baseline, which list approved and rejected patches and can contain rules that can automatically approve patches after they have been out for a certain number of days
    - Parameter Store
        + Provides the ability to not only securely store or call secrets but also store items like database strings and license code
        + Also has the ability to use versioning to allow retrieval of old passwords
    - Session Manager
        + Allows you to connect remotely to your EC2 managed instances with no exceptions needed in the security group for that remote access
    - State Manager
        + A compliance tool allows you to ensure your instances are running the appropriate versions of software, define security group settings that are permissible and join Windows systems to a domain, or run scripts against Windows and Linux systems