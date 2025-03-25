Assessment Test

1. Your senior administrator has asked you to set up notifications for the AWS Budgets configuration in the organization's developer accounts.  Which of the following notification  options are available for AWS Budgets? (Choose two)

A. Posting to the Personal Health Dashboard
B. Amazon SNS topics
C. AWS Management Console notifications
D. Direct integration with ServiceNow
E. Direct email recipients

Answer:  B.E.

Explanation:  When configuring AWS Budgets for notifications, you can select from emailing up to 10 recipients directly from the budget configuration.  You can also use Amazon SNS to send SMS messages or take other actions through event triggers with Lambda.

Book Entry: CH 3 Page 95

2. THe two strategies for cache loading include which of the following? (Choose two)

A. Arbitrary acquisition
B. First-in, first-out (FIFO)
C. Lazy Loading
D. Least effort load
E. Write-through

Answer:  C./E.

Explanation:  In write-through caching any data destined for the database is also written to the cache.  The advantage here is that data in the cache is always the most current.  This model takes more resources to write both the databases.  In lazy loading caching only populates the database with data that has actually been requested.  This keeps the cache sizes smaller and more relevant.

Book Entry: CH 7 Page 296

3. The compliance officer for the organization has asked you to confirm the maximum length of historcal data that AWS Cost Explorer provides.  Which of the following options will you provide to the compliance officer?

A. 24 months
B. 36 months
C. 18 months
D. 12 months

Answer:  D.

Explanation: AWS Cost Explorer provides current month, prior 12 months, and the ability to forecast the next 12 months of AWS cost and usage using the same dataset as the AWS Cost and Usage reports.

Book Entry: CH 3 Page 88


4. Why might you use a geoproximity routing policy rather than a geolocation routing policy?

A.  You want to increase the size of traffic in a certain region over time.
B.  You want to ensure that all US users are directed to US-based hosts
C.  You want to route users geographically to ensure compliance issues are met based on requestor location
D.  You are concerned about network latency more than requestor location

Answer:  A.

Explanation:  A geoproximity, like a geolocation policy, routes users to the closest geographical region.  This means that option B and C are incorrect, as they are common to both types of routing policy.  Option D would imply the use of latency-based routing, leaving only option A.  This is the purpose of a geoproximity policy: you can apply a bias to adjust traffic to a region

Book Entry: CH 10 Page 407/408

5. In Auto Scaling, what does the desired capacity refer to?

A. The average capacity that the customer expects to need over the next billing cycle
B. The capacity that the customer expects to need over the next billing cycle
C. The initial capacity of the Auto Scaling group that the system will attempt to maintain
D. The lowest capacity of the Auto Scaling group at which the workload is still able to perform

Answer:  C.

Explanation:  There are three limits that are set for an Auto Scaling group: the minimum, desired, and maximum capacities.  The minimum is the smallest acceptable group size. The maximum is as large as the group will be allowed to scale.  The desired is the initial size of the group.  Auto Scaling then attempts to maintain that size. When demand causes the group to scale out, Auto Scaling will then scale in at the end of the event back to the desired capacity.

Book Entry: CH 5 Page 218

6. You have an application deployment with endpoints in multiple countries.  The application needs to have fast response times, and in the event of a failure, you cannot modify the client code to redirect traffic. Which service can help you implement a solution?

A. Amazon ElastiCache
B. Route 53
C. Amazon CloudFront
D. AWS Global Accelerator


Answer:  D.

Explanation: The anycast IP addresses provisioned by AWS Global Accelerator will allow you to reach a health endpoint without having to switch IP addressing, modify the client code, or be concerned about DNS caching.

Book Entry: CH 10 Page 420

7. You are securing resources in your VPC.  You wish to allow only specific ports and you require stateful connections.  Which of the following best fulfills these requirements?

A. NAT Gateway
B. Network access control lists (NACLs)
C. Security Groups
D. Web Application Firewall (WAF)

Answer:  C

Explanation: A NAT gateway is used by resources in a private subnet to initiate communication with the Internet.  A WAF monitors and protects HTTP(S) requests.  NACLs and security groups are very similar, and you will need to know the differences.  The security group is stateful and the NACL is stateless.  Additionally, the question only asks for traffic to be allowed with no requirement for deny rules.  NACLs allow deny rules.  Given the choice between a secruity group and an NACL, the security group is the preferred method if all else is equal. 

Book Entry: CH 9 Page 368

8. Which of the following saves you from provisioning keys to operate AWS services in a programmatic way?

A. The AWS Management Console
B. AWS CloudShell
C. Session Manager
D. IAM groups

Answer:  B

Explanation: AWS CloudShell provides a mechanism for operators to use the AWS CLI without having to provision access keys in a local machine.  This adds a new layer of security as it saves time and effort in executing one-line and simple administrative CLI commands

Book Entry: CH 1 Page 10

9. You oversee monitoring of performance for several production data conversion systems running on Amazon EC2 instances.  Recently the data engineers reported below normal write and read speeds coming from several application servers.  Each application server is a T3.Large using gp2 EBS Volumes for the operating system volume and St1 volumes for the data processing volumes.  You are concerned that the volumes are throttling.  Which Amazon CloudWatch EBS volume metric will confirm EBS volume throttling?

A. VolumeQueueLength
B. VolumeWriteOps
C. VolumeReadBytes
D. BurstBalance

Answer:  D

Explanation:  In this scenario the data engineers are reporting below normal write and read speeds, which is a great indicator that the volume is throttling.  The EBS volumes used in this deployment are gp2 and st1 volume types, which both use burst bucket balance to maintain performance above the baseline available IOPS for the volume.  Checking for depletion of the BucketeBalance metric for the volume can identify depletion of the burst bucket and result in low performance for the EBS volume.

Book Entry: CH 6 Page 256

10. Inline IAM policies are best use when:

A. Inline policies are not recommended
B. Customer-managed policies must be kept secure
C. An appropriate AWS-managed policy does not exist
D. Resource-based policies must be tightly integrated with identity-based policies

Answer:  A.

Explanation: While inline policies are available as an option, they are not recommended.  Inline policies can be difficult to troubleshoot, and there are almost always better options.

Book Entry: CH 2 Page 56

11. Your organization is undergoing an application modernization effort and focusing on decommissioning and consolidating applications on-premises into a new AWS environment.  Several applications require the use of Secure File Protocol (SFTP) to move files between the application server and the customer.  To reduce cost and assist with consolidation, you want to move all SFTP servers into AWS.  Which AWS service provides the most scalable and cost effective solution?

A. Amazon EFS
B. AWS Transfer Family
C. AWS DataSync
D. Amazon EC2

Answer:  B.

Explanation:  In this scenario the organization is looking for a scalable and cost-effective solution to migrate SFTP servics from on-premises to the AWS Cloud.  This automatically eliminates the option of using Amazon EFS and AWS DataSync as they do not offer a method of enabling SFTP.  Amazon EC2 is a potential option but would require custom configuration of an SFTP server on Amazon EC2, including the need for configuring scaling using Auto Scaling. This increases the overall cost and complexity of the solution.  The most cost-effective and scalable option is to use AWS Transfer Family, which is managed service that lets you configure an SFTP service that scales to meet customer demand; AWS manages the underlying infrastructure.

Book Entry: CH 6 Page 272

12. Which AWS services have CLI wizards available? (Choose three)

A. Amazon EC2
B. AWS Lambda functions
C. Amazon DynamoDB
D. AWS IAM
E. Amazon RDS
F. Amazon S3

Answer:  B./C./D.

Explanation:  Wizards will query existing resources and prompt you for data in the process of setting up for the service invoked.  As of this writing, wizards are available for configure, dynamodb, iam, and lambda functions.

Book Entry: CH 1 Page 20

13. You have been contacted by the security team because they are receiving too many findings from Macie in Security Hub.  The security team has asked if it is possible to change the frequency of findings being sent into Security Hub from Macie.  Which of the following frequencies are supported by Macie? (Choose three)

A. 15 minutes
B. 5 minutes
C. 1 hour
D. 3 hours
E. 6 hours
F. 30 minutes

Answer:  A./C./E.

Explanation:  Macie allows customizable frequencies for when findings are published to Security Hub.  You can update the publication setting to fit the needs of the security team by adjusting the findings publication fromm the default of 15 minutes to either every one hour or every six hours.  If you modify the publication timings within one region, you will need to modify every other region where Macie is in use as well.

Book Entry: CH 4 Page 151

14. A company wants to analyze the click sequence of their website users.  The webiste is very busy and receives traffic of 10,000 requests per second.  Which service provides a near-real-time solution to capturing the data?

A. Kinesis Data Streams
B. Kinesis Data Firehose
C. Kinesis Data Analytics
D. Kinesis Video Stream

Answer:  A

Explanation: This is a classic use case for Kinesis Data Streams

Book Entry: CH 11 Page 451

15. Which of the following statements about RDS read replicas is true? (Choose two)

A. A replica  can be promoted to replace the primary DB instance
B. Read replicas are used as read-only copies of the primary DB instace
C. Read replicas should be created in a different VPC from the primary DB instance
D. The read replica and primary DB instance replicate synchronously

Answer:  A./B.

Explanation:  Replication between the primary and read replicas is asynchronous.  Creating a read replicas in VPCs outside of the primary instance's VPC can create conflicts with the CIDR.

Book Entry: CH 7 Page 290

16. Your workload spikes every Thursday evening while batch processing runs, and processes are frequently throttled as soon as processing beings.  Which of the following scalling methods will most effectively solve this problem?

A. Predictive scaling
B. Simple scaling
C. Step scaling
D. Target tracking

Answer:  A.

Explanation:  While simple, step, and target tracking scaling will scale out the workload, they only begin scaling after the metric indicates a problem.  Predictive scaling anticipates the event based on historical data and scales out ahead of the Thursday evening batch processing so that throttling is avoided.

Book Entry: CH 5 Page 221

17. The principal of trust between two unrelated networks is known as

A. Distrbuted computing
B. Federation
C. Hybrid computing
D. Interoperability

Answer:  B.

Explanation:  Federation is a trust between two parties or systems for the purpose of authenticating users and conveying information needed to authorize their access to resources.  Distributed computing is, at its most fundamental, just computing between two or more computers via messaging usually along a network.  It does not imply trust.  Hybrid computing refers to a combinatin of cloud and on-premises resources.  Again, no trust is implied.  Interoperability is the ability of one computer or application to talk to another.  Standards and protocols provide us with interoperability but do not imply trust

Book Entry: CH 2 Page 51

18. Which of the following does Elastic Beanstalk store in S3? (Choose two)

A. Server log files
B. Database swap files
C. Application files
D. Elastic Beanstalk log files

Answer:  A./C.

Explanation: Elastic Beanstalk will store application files and server log files in S3

Book Entry: CH 11 Page 430

19. You have been tasked by the CISO to protect all web applications in the production AWS account from SQL injection attacks and cross-site scripting.  Which AWS service will you use to accomplish this goal?

A. Amazon VPC security groups
B. AWS Web Application Firewall
C. AWS Network Firewall
D. AWS Shield

Answer:  B.

Explanation: The AWS Web Application Firewall (AWS WAF) is a layer 7 firewall used to protect your web applications form DDoS attacks, SQL injection attacks, and cross-site scripting attacks.  You can also allow, block, or count web requests coming into an application based on criteria that you set, such as IP addresses, geolocations, and HTTP headers.

Book Entry: CH 4 Page 169

20. You wish to allow administrators to securely connect to hosts in a private subnet in your VPC.  Which of the following will best solve this problem?

A. Bastion Host
B. Client VPN
C. NAT Gateway
D. Transit Gateway

Answer:  A.

Explanation:  The NAT gateway and bastion host are often confused.  A NAT gateway allows communication out, whereas a bastion host allows communication in.

Book Entry: CH 9 Page 378