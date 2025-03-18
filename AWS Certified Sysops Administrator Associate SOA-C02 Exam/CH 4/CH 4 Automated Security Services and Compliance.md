CH 4 Automated Security Services and Compliance

1. Understand how to review Trusted Advisor security checks
    - There are 4 types of plans with Trusted Advisor
        + Basic
        + Developer
        + Business
        + Enterprise
    - The Basic and Developer Plans have access to the free tier Trusted Advisor Checks
        + IAM Use
            ++ Checks for the use of IAM users, groups, and roles in AWS
        + MFA on Root Account
            ++ Verifies that the root account has MFA enabled and issues an alert if the feature is not enabled
        + Security Groups - Specific Ports Unrestricted
            ++ Checks security groups for rules that allow unrestricted access (0.0.0.0/0) to specific ports like thos used for remote management
        + Amazon S3 Bucket Permissions
            ++ Check verifies that no S3 bucket is allowing open-access permissions (Public) or allowing access to any unauthenticated AWS user
    - The Business and Enterprise Plans have access to the free tier plans plus the following checks
        + Amazon EC2 Instances with Microsoft SQL Server End of Support
            ++ Check alerts if the versions of Microsoft SQL Server are near or have reached end of support
        + Amazon EBS and RDS Public Snapshots
            ++ These are two separate checks that verify permission settings and alerts of any snapshots marked as public
        + Amazon RDS Security Group Access Risk
            ++ Check helps keep databases running on Amazon RDS instances from potentially overly permissive security groups
        + Amazon Route 53 MX Resource Sets and Sender Policy Framework
            ++ Check verifies that each MX record set has a TXT or SPF resource record created with a valid SPF record
        + AWS CloudTrail logging
            ++ Check verifies that CloudTrail is enabled and wether it is in use across multiple regions
        + AWS Lambda Functions Using Deprecated Runtimes
            ++ Provides details on Lambda functions that are running on deprecated or soon-to-be-deprecated runtimes
        + AWS Well-Architected High-Risk Issues for Security
            ++ Checks workloads for High Risk Issues (HRIs) based on the Well-Architected Framework
        + CloudFRont Custom SSL Certificates in the IAM Certificate Store
            ++ Check looks at custom SSL certificates for CloudFront alternate domain names and alerts when a certificate is expired, about to expire, using outdated encryption methods (SHA-1 hashing), or has a misconfiguration such as the certificate not containing the origin domain name or the domain name
        + CloudFront SSL Certificate on the Origin Server
            ++ Verifies origin server SSL certificate expiration and encryption use
        + ELB Listener security
            ++ Checks load balancers for listeners that are not configured using recommended security configurations for encrypted communications
        + ELB Security Groups
            ++ Check verifies that load balancers are not missing and assigned security group or that have security groups that allow access to ports that are not configured on the load balancer
        + Exposed Access Keys
            ++ Check evaluates common code repositories for AWS access key that may have been exposed to the public.  AIs looks for EC2 usage that could be a result of a compromised access keys
        + IAM Access Key Rotation
            ++ Check verifies that IAM access keys are rotated in the last 90 days and produces an alert for any IAM keys that have not been rotated.
        + IAM Password Policy
            ++ Check provides alerts when a password policy is not enabled or if password content requirements have not been enabled
        + Security Groups - Unrestricted Access
            ++ Check evaluates security groups for rules that allow unrestricted access to a resources and could potentially increase malicious activity opportunities like denial of service attacks or hacking

2. Understand Security Hub Findings and reports
    - Security Hub provides a centralized location to review findings from AWS accounts, AWS services, and supported third-party partners.  Security Hub helps you analyze security trends and identifies the highest-priority security issues you should address within your AWS account that are visible using aggregated findings in prebuilt dashboards.
    - Security Hub use pre-packaged security standards to help evaluate the security posture of an AWS account.
    - The first step in using Security Hub is to enable it in the region where you want to consume findings from enabled services like GuardDuty, Macie, Inspector.
    - Findings from the other services are grouped together into insights in Security Hub.  Insights are collections of findings grouped by filter and help identify common security issues that may require remediation actions.  YOu can create custom insights or use predefined AWS managed insights to determine remediation actions.
    - Security Hub also allows you to track the current status of investigations within a finding.  Each finding has a workflow status, which tracks the progress of the investigation into a finding.
    - Security Hub can use custom actions to automate remediation tasks using Amazon EventBridge.  This integration allows you to use AWS services to perform remediation actions in response to system events.  Security Hub automatically sends all new findings and all updates to existing findings to EventBridge as EventBridge events.
    - Disabling Security Hub can be accomplished from the Security Hub console or by using the Security Hub API.  Before you disable Security Hub, you must disassociate the account from the administrator account, which can only be done by the administrator account.

3. Understand GuradDuty threat detection findings
    - GuradDuty analyzes continous metadata streams generated from your account and any network activity found in CloudTrail events, VPC flow logs, and DNS logs.  GuardDuty uses machine learning to accurately identify threats within your account and it operates completely independently from your other resources and workloads.
    - GuardDuty does not have an up-front cost associated with the service but does operate using the same pay-as-you-go model that other serviecs use.  You only pay for the events analyzed with no additional software to deploy or threat intelligence subscriptions required.
    - GuardDuty is a regional service, and any configurations must be replicated to each region that you wish to have monitored.
    - A service-linked role for your account is created called AWSServiceRoleForAmazonGuardDuty.  This IAM role inclueds permissions and trust policies that GuardDuty requires to consume and analyze events.
    - GuardDuty can monitor object-level API operations when S3 protection is enabled.  S3 protection helps identify potential security risks for data stored in your S3 buckets
    - Any S3 objects that you have made publicly accessible will not be processed by GuardDuty; however, it will alert when a bucket is made publicly accessible.
    - GuardDuty offers Kubernetes protection, which enables the detection of suspicious activities and potential compromises in your Kubernetes clusters with EKS.
    - There are 3 types of findings in GuardDuty
        + Findings for EC2 resources
            ++ Will always have a resource type of Instance.  GuardDuty will assign a resource role, which indicates if a EC2 instance was the target or the instigator of the activity.
        + Findings for S3 resources
            ++ S3 resources will have a resource type of S3 Buckets when related to S3 CloudTrail data event data source, or a resource type of AccessKey if related to the CloudTrail management event data source.
        + Findings for IAM
            ++ Are specific to IAM entities and access keys and will have a resource type of AccessKey.
            ++ GuardDuty uses the following IAM finding types:
                +++ CredentialAccess
                +++ DefenseEvasion
                +++ Discovery
                +++ Exfiltration
                +++ Impact
                +++ InitialAccess
                +++ PenTest
                +++ Persistence
                +++ Policy
                +++ PrivilegeEscalation
                +++ Recon
                +++ Stealth
                +++ UnauthorizedAccess
    - GuardDuty findings are assigned different security levels and values that reflect the potential risk the finding could have within your environment
        + High Severity issues 9.0 to 7.0 indicate a resource may be compromised and requires immediate action
        + Medium Severity issues 6.9 to 4.0 indicate suspicious activity that deviates from normal behavior and investigation at earliest convience is advised.
        + Low Severity issues 3.9 to 1.0 indicate attempted suspicious activities that did not compromise the network or result in an intrusion.  Doesn't require immediate attention but should evaluate for a false positive.

4. Be able to review findings in Inspector
    - Inspector offers automated discovery and continual scanning to deliver near-real-time vulnerability findings all controlled by a centralized management, configuration, and view of findings within the Inspector Console.
    - You will be charged montly based on a combination of two dimensions: the number of  EC2 instances being scanned, and the total number of container images initially scanned when sent to ECR or rescanned during a month.
    - This is a regional service and must be configured for each region that has resources you want scanned.  Inspector uses Systems Manager (SSM) agents installed and enabled on EC2 instances to provide common vulnerabilities and exposures (CVEs) vulnerability data.
    - Enabling Inspector will create a globally-service-linked role name AWSServiceRoleForAmazonInspector2.  This role is what allows Inspector to collect and analyze VPC configurations and software package information to generate vulnerability findings.
    - Inspector creates detailed finding reports.  Each finding is titled according to the detected vulnerability and provides other useful information such as serverity rating, information details about the affected resource, and additional details on how to remediate the reported vulnerability.
    - In the Inspector console you can assign finding the following statues:
        + Active: The finding has not yet been remediated or surpressed because of the use of suppression rules
        + Suppressed: Findings that need to be hidden from most views
        + Closed: Any findings that remediated will be detected automatically and changed to closed
    - Types of Findings
        + Package vulnerability Finding: writes about exposed software packages to CVEs
        + Network Vulnerability: Indicates allowed network paths to EC2 instances in your environment
    - Findings Summary section allows you to see all occurences of a finding and then dig deeper into specific rows to view an overview of the finding, including the AWS account in which the impacted resources reside, the severity, vulnerability type, and when it was last detected.
    - Each finding will also be given a serverity level by Inspector findings.  The serverity ratings are represented as Untriaged, Informational, Low, Medium, High, and Critical.
    - In the Inspector Console you can view and manage findings using groupings based on specific parameters like finding state, vulnerability, account, EC2 instance, container image, or repository
    - Inspector offers a dashboard to view snapshot statistics for your resources.  Shows metrics about resource coverage and active vulnerabilities, serving as an overview for Inspector health and quick glance reporting
    - The Enviornment Coverage Section shows statistics about the resources that Inspector scans
    - The Critical Findings section shows a count of critical vulnerabilities in your environment.
    - The Risk-Based Remediation shows the top five software packages with critical vulnerabilities in your environment and allows you to choose a package name to see additional associated details and impacted resources

5. Understand how to implement encryption at rest using AWS KMS
    - AWS KMS is a highly available Key Generation, storage, management, and auditing service for AWS account owners to encrypt or digitally sign data. Allows you to encrypt and digitally sign data within your own applications or control encryption of data across AWS services through integration.
    - Pricing follows the same model as other services using pay-as-you-go
    - You have control over the life cycle and permissions of the KMS key which means you can determine who will be able to use or manage the key once it is generated.
    - You can always import your own key material and associate it with the KMS Key if your security policies or organization require this
    - Once the key material is generated by KMS, you can submit data directly to the service for signing encryption, or decryption using this new KMS key
    - When creating key you must decide between using a symmetric key or an asymmetric key
    - KMS has a limit of 4 KB of data that the service can directly encrypt or decrypt.  To encrypt larger datasets using KMS keys, you will use a practice called envelope encryption.
    - Envelop Encryption is the process of encrypting plaintext data with a data key, and then encrypting the data key with another key.
    - When creating an IAM policy for a user or principal who requires key creation permissions in KMS, you must confirm that KMS: CreateKey is included in the IAM policy.  If your data protection strategy requires the use of aliases or tags, you will also need to ensure that KMS:CreateAlias and KMS:TagResources is in the policy
    - KMS keys belong to the account that created the key not the user
    - While it is optional for a KMS key to have IAM policies and grants to control key access, every KMS key must have a  key policy, which differes from IAM policy as the key policy is regional.  It is important to note that every principal, including the key creator, does not have permissions to a key unless explicitly allowed in a key policy, IAM policy, or grant.
    - If a principal is denied anywhere in a key policy or IAM policy, they will never gain access to the kye
    - The key policy has a built-in protections to ensure that the keys do not become unmanageable, this is the default policy statement.  If allows the account to use IAM policies to allow access to the KMS key, as well ass the key policy itself.
    - Key rotation can be done manually or you can do automatic rotation.
    - Automatic rotation means KMS manages key generation and saves all previous versions of the cryptographic material
    - Key rotation changes only the KMS key's key material
    - The key ID stays the same and your applications do not need to change to refere to a new key ID or alias.
    - Various services like EBS, S3, and AWS Systems Manager Parameters Store use KMS to encrypt at rest.
    - S3 offers to KMS-related methods for encyrpting data within an S3 Bucket:
        + Option 1: Use the AWS Key Management Service Keys (SSE-KMS) allows AWS to manage the KMS key in its entirety including rotation and permissions
        + Option 2: If you need to rotate keys more frequently or manage key creation yourself you can use your own AWS KMS key

6. Know how to implement encyrption in transit using AWS Certificate Manager
    - AWS Certificate Manager (ACM) is an AWS integrated service that offers provisioning and renewing of TLC/SSL certificates
    - ACM can be deployed on AWS resources such as elastic load balancers, CloudFront distributions, and API endpoints on API Gateway
    - Certificates generated by ACM are also capable of being used for private internal resources to verify identity of resources on a private network
    - WHen issuing certificates you will need to configure ACM Private Certificate Authority (CA) which handles the issuance, validation, and revocation of these private certificates
    - ACM provides the ability to import third-party certificates into the ACM management system to simplify certificate management for applications that require third-party wildcard, singluar, or multiple specific domain names used by your applications in AWS.  The largest benefit of ACM is the automated renewal of expiring certificates managed by the service.
    - ACM requires that you have a registered fully qualified domain name (FQDN) that can be hosted in Route 53 or any of the commercial registrars available today.  You can validate using email validation or using a Certificate Authority Authorization (CAA) DNS record.
    - ACM will not provide renewal services for imported certificates
    - Importing a third-party certificate signed by a non-AWS CA, you must also include the private key, the certificate, and the public certificate chain.
    - Certificate Manager supports the use of  CloudWatch metrics and CloudWatch events to perform notifications and take automated actions against ACM certificates
    - ACM by itself isn't enough to encrypt traffic in transit; it is just the source of the certificates used to encrypt the data in transit.
    - Two of the most used services that integrate with ACM to provide encryption in transit are ELB and CloudFront
    - ELC requires the certificates to be installed on either the ELB or the backend EC2 instance
    - CloudFront requires the certificates to be installed on the distribution or on the backend content source (origin) 
        + To use ACM with CloudFront you must request or import the certificates in the US East Virginia Region
    - All network traffic between AWS datacenters is transparently encrypted at the physical layer, and all traffic within a VPC and between peered VPCs across regions are transparently encyrpted at the network layer. AWS also encrypts all data in transit at the AWS service endpoints by using TLS to create a secure HTTPS connection for API requests
    - Its the choice of the customer to encrypt data in transit at the application layer

7. Know how to enforce data classification scheme with Macie
    - Macie uses machine learning and pattern matching to discover and protect sensitive data stored in S3 buckets, at scale.  Macie can identify several types of sensitive data and even data unique to your organization
    - Pricing for Macie follows a per month, per bucket, and per gigabyte of data processed model.
    - Macie is a regional service and needs to be enabled in each region in which you want to scan S3 buckets for sensitive data and security controls
    - To scan S3 Buckets you must configure and run data discovery jobs.  Data discovery jobs scan and analyze objects in S3 Buckets found during the inventory scan that you select to determine if sensitive data is present
    - The Macie dashboard provides sensitive data discovery results for 90 days.
    - There are three types of accounts associated with Macie
        + Administrator Account: Centrally manages all Macie accounts that are associated with each other
        + Member accounts: Centrally managed as a group within a specific AWS region
        + Stand-alone accounts: Account not part of an organization
    - Macie uses an IAM service-linked role not part of an organization in the current AWS region.  The IAM policy allows Macie to call other services on your behalf and monitor resources.  This role also allows Macie to conduct the inventory of the S3 buckets in the region and evaluate the security and access controls for these buckets
    - Macie uses CloudTrail events as a source of information to evaluate buckets security and privacy
    - Custom data identifiers allow you to define a set of criteria to detect sensitive data that is unique to your needs using a regular expression (regex).  You can define which patterns or sequences you want Macie to match based on regular expressions to reflect your ogranization's sensitive data detection needs
    - Once you have decided which data identifier type you want to use for scanning sensitive data within your buckets, you must define a schedule and scope of the job analysis.
    - Reviewing findings with Macie can occur in a few places
        + Macie Console Findings Page: Used for a quick glance analysis and groupings, filtering, and creating suppression rules for improving future analysis
        + Macie API: Used to query and retrieve the findings data using HTTPS request
    - Macie supports integration with services like EventBridge and Security Hub
    - You can create a data discovery job to scan S3 buckets.  These jobs findings can then be reviewed in the Macie console or automation through EventBridge to send the findings and notifications to the security team without requiring manual intervention
    - Macie isn't enforcing data to be classified or provides a method for moving data into a classification itself. Rather Macie findings allow you to locate the potential issues and use other services for remediation

8. Understand how to securly store secrets in Secrets Manager
    - Secrets Manager can natively rotate credentials for RDS, DocumentDB, and Redshift clusters
    - Secrets Manager requires an IAM policy permission in order for applications to access specific secrets and the Secrets Manager service.
    - Secrets Manager encrypts secrets at rest using KMS keys that you own and store in the KMS key to decrypt the secret and transmit it using TLS to your local environment and application
    - Secrets Manager follows the pay-as-you-go pricing model where you only pay for what you use with no minimum or setup fee.
    - There are four ways to access secrets stored in Secrets Manager:
        + Using the Secrets Manager console
        + Using the CLI
        + Using the AWS SDK
        + Using HTTPS Query API
    - To access secrets stored in Secrets Manager, you must ensure that the user, group, or role has the appropriate IAM permissions
    - Monitoring the use of Secrets Manager has two methods
        + CloudTrail captures API calls and related events made to the Secrets Manager service on behalf of your account and delivers the log files into an S3 bucket
        + CloudWatch is used to identify and alert when your request rate for APIs reaches a specified threshold
    - Secrets Manager also integrates with EventBridge for notification of certain events that impact secrets within your account.
    - Parameters needed to set a Secret
        + Type of Database store
        + Select an encryption key that Secrets Manager uses to encrypt the secret value
        + Choose database that they secret is related to
        + Secret name
        + Description
        + Opptionally
            ++ Tags
            ++ Creation of resource permissions
            ++ Replication
            ++ Rotation
    - There are several ways to retrieve secrets
        + AWS Management Console
        + AWS SDK
        + AWS CLI
    - To limit the number of API request to Secrewts Manager, improve speed, and reduce costs, you should use client-side caching within any of the AWS SDKs

9. Be able to configure AWS network proctection services using AWS Shield
    - AWS Shield  is a managed service that provides protection against DDOS attacks for your applications running on AWS
    - There are two Shield versions
        + Shield Standard: Automatically enabled for all accounts at no additional cost
        + Shield Advanced: Paid service with extra benefits
    - Shield Standard offers protection for all AWS customers against common and frequently used network attacks occuring at the network layer and transport layer of a network.  Shield Standard protects against attacks like SYN/UDP floods and reflection attacks to support high availability of applications running in AWS
    - Shield Advanced offers enhanced protection for applications running on AWS services.  It also covers edge services like Global Accelerator and Roue 53 resources against larger and more sophisticated attacks using always-on and flow-based monitoring of network traffic and active application monitoring
    - Any customers that are Business and Enteprise support subscribers can engage with the Shield Response Team (SRT) which provides 24x7 support
    - Shield Advanced also has DDOS cost protection, which protects against scaling costs associated with mitigation efforts when responding to DDOS attacks
    - Shield Advanced has a $3,000 monthly fee with a one year commmitment
    - Shield Advanced integrates with AWS WAF and uses WAF ACLs, rules and rule groups to provide application layer protections.  The subscription includes the WAF basic fees for web ACLs, rules, and web requests.  Includes automatic application layer DDOS mitigation by creating, evaluating, and deploying custom AWS WAF rules for protected resources.
    - Shield Advanced helps prevent false positives and provides faster detection and mitigation when a potential resource is unhealthy and using Route 53 health checks
    - Monitoring, management, and visiblity is also increased when using Shield advanced.  It provides access to real-time metrics and reports for events and attacks or resources protected by Shielf Advanced.
    - Subscribers receive additional information about the events and DDOS attacks against resources protected.
    - Advanced offers the ability to see cross-account events when combined with the usage of Firwall manager to manage Shield Advanced protections

10. Understand how to configure AWS network protection services using AWS WAF
    - AWS WAF helps protect web applications from attacks by using configurable roles that can allow, block, or count web requests coming into your web application based on definable conditions.  You can define conditions to include in rules based on IP addresses, HTTP headers, HTTP body, URI strings, SQL injection, and even cross-site scripting.
    - Provides visiblity and control over common pervasive bot traffic attempting to access your web applications
    - You can use custom rules and managed rules at the same time to protect your application by allowing more customization and protection
    - WAF follows a pricing model that charges based on the number of web access control lists (web ACLs) that are created in your account.  You are also charged by the number of web requests that are received by AWS WAF.
    - AWS WAF uses web ACLs to procted AWS resources, and you define what is blocked in each web ACL rule.  These rules are the statements of conditions that AWS WAF uses to inspect the web requests and to decide whether to bock, allow, run CAPTCHA, or count transactions
    - When applying rules to a web ACL, you also configure the actions AWS WAF uses to handle the matching web request
    - Once a match is found and the action is to allow or block the request the web ACL has done its job it stops looking for a match
    - There are nonterminating actions such as counting and CAPTCHA. Counting is logging the requests that meet the required conditions
    - WAF also allows overriding of actions of a rule or group of rules to alter terminating rules by adding a count action instead of allowing or blocking the request
    - Rule groups are reusable set of rules that can be added to a web ACL.  There are three categories of rule groups:
        + Managed: Are collections of ready-to-use and preconfigured rules that AWS and various AWS Marketplace sellers design and maintain
        + Custom: Rule groups made by you
        + Integrated: Rule groups owned and managed by other services like Firewall Manager and Shield Advanced
    - Rules must have one top-level statement, which can contain nested statements at any depth depending on the rule and statement type
    - Statements can also use logical statments AND, OR, and NOT to combine statements in a rule
    - Rules cannot exist on their own and are not considered a resource.  They do not have an ARN and cannot be independently accessed
    - Rule names must be unique to every rule in the web ACL or rule group, and cannot be changed after creation
    - Rules can include a scope-down statement to further narrow the scope of requests that the rule evaluates. A scope-down statement will evaluate the request against the scope-down statement first, and if a match is found it will continue using the rules standard criteria.
    - AWS WAF Bot Control is used to help manage bot activity coming into your site by categorizing and identifying common bots, verifying desirable bots, and detecting high-confidence signature bots
    - Bot Control has six basic components
        + Managed Rule Group
        + Bot Control Dashboard
        + Logging and metrics
        + Scope-down Rules
        + Labels and label matching rules
        + Custom Request
        + Responses
    - WAF also has Fraud Control ATP, which helps prevent account takeover by gaining unauthorized access to a person's account.  ATP provides visibilty and control over anomalous login attempts that may be from stolen credentials
    - When using AWS-managed rule groups that enabled advanced managed integration, you need to integrate the AWS WAF SDK into your application.  These advanced managed integration rule groups require an SDK integration or for you to provide security capabilities that are enhanced by the integration
    - To assist in weeding out unwanted requests and limiting the ability for non-human logins, you can implement the WAF CAPTCHA component
    - WAF helps round out the network protection by controlling traffic at the edge and limiting web requests to only what you specify for the application
    - You still need to implement other network protections such as Shield, Shield Advanced, Firewall Manager and even basic protection like security groups and CloudFront to protect the server origin