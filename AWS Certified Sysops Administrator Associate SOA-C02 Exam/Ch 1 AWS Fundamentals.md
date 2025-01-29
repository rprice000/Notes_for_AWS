Ch 1 AWS Fundamentals

Exam Essentials

1.  Know how to create an AWS account and secure the root user
    - To create an account you will need
        + email address
        + unique account name
        + password
        + specify if account is business or personal
        + name
        + address
        + phone number
        + credit card
        + support plan
        + web browser
    - To secure root user
        + Implement MFA for all accounts
        + Do not use root account after for basic creation and setup
        + Define account level password policy
            ++ NOTE:  The root account falls out of scope of IAM policies
        + Use CloudShell for CLI commands where applicable
        + Use Session Manager to connect to EC2 instances
        + Use IAM Roles
        + Know how to get help
            ++ Documentation
            ++ Support Forums
            ++ AWS Support Center

2.  Understand how to use the AWS Management Console and CLI
    - Console Menu Items
        + Console Home Icon: Used to return to the main landing page as you navigate into different AWS services
        + Services Icon:  Used to view all services by category or alphabetically
        + Search Icon:  Used to search for a service by name or substring
            ++ AWS Resource Explorer:  Managed feature that simplifies search and discovery of resources like EC2 instances across regions in your AWS account
        + CloudShell Icon:  Amazon Linux 2 environment preconfigured to allow you to explore and manage AWS services from a terminal in your browser
        + Notifications Icon:  Gives you visiblity to open issues scheduled changes, event log, and any other notifications AWS sends to your console for clarity and information
        + Support Icon:  Gives you access to the AWS Support Center, Expert Help Landing Page for AWS IQ, AWSre:Post community forums, AWS Documentation, AWS Training Page, Getting Started Resource Center and Send Feedback About your Experience
        + Settings Icon:  Used to define the settings for your current users
        + Region Icon: Displays your current operating region
        + Account Icon:  Displays account name and number, Navigation for account configuration settings, AWS Organizations, Service Quotas Page, Billing Dashboard and Identity Management, and Unified Account Settings
    - The CLI provides tools used from the command-line terminal.  It can be installed on Linux, MacOS, and Windows machines.
    - There is CloudShell in the Management Console which provides the same capabilities as the CLI on a local machine
    - After installing the CLI locally you need
        + Run the 'aws configure' command
        + Provide access key ID, secret access key, default region, default output format
            ++ NOTE:  Access key and secret key must exist before configuring the CLI locally
    - There is a version 2 of the CLI called CLIv2
    - CLIv2 no longer requires python to be pre-installed prior to installing CLI locally
    - AWS CLIv2 has a wizards feature which is an improved version of the -cli-auto-prompt command line option
    - Wizards will query existing resources and prompt you for data in the process of setting up for the service involved
    - CLI output default is a JSON Document
    - You can choose output to be tab-delimited "text" output
    - The CLI --query option is used to limit the results displayed in the CLI
    - The --filter option used to manage displayed results
    - The --dry-run used to verify you have the required permissions to make request and gives you an error if you are authorized

3.  Be familiar with the AWS Personal Health Dashboard
    - There are two versions of the AWS Health Client Dashboard.  The first version is the public AWS Health Dashboard.  It is used to gain visibility to the health of all AWS services.  The page displays any reported service event for services across regions.  You are not required to have an AWS account to access the AWS Health Dashboard.
    - The AWS Personal Health Dashboard gives you a personalized view of the performance and availability of the AWS services you're using.
    - You can configure your Personal Health Dashboard to use local time zone settings for published events and receive notifications and detailed remediation guidance when AWS is sustaining a service event that may have an impact on your implementation.
    - The AWS Health API is available directly as part of an AWS Business or Enterprise Support Plan.  Allows for integration with Slack, Teams, Amazon Chime, and other partners like Datadog and Splunk.
    - AWS Health Aware (AHA) solution is provided by AWS and is available in GitHub AWS Sample repos.  AHA implements a serverless infrastructure using CloudFormation that sends alerts from the AWS Health API to your chosen communication channels to actively monitor and respond to AWS Health events.

4.  Understand the AWS global infrastructure and all components
    - Region:  This is a physical location in the world where AWS has clusters of datacenters.  Regions are composed of availability zones
    - Availability Zones:  This is a logical group of datacenters.  These groups are isolated and physically separate.  Each of them includes independent power, cooling, physical secruity, and interconnectivity using high bandwidth and low-latency links.  All traffic between AZs is encrypted. Also, each AS is implemented separately from other AZs but within 60 miles of each other
    - Edge Location:  This is the resource used by AWS to deliver reliable and low-latency performance globally.  Edge locations are how AWS attains high performance in countries and territories where a region does not exist.
    - Local Zones:  This is an extension of a region where you can run low-latency applications using AWS services in proximity to end users.  Local zones deliver single-digit milisecond latencies to users for use cases like media entertainment, and real-time gaming, among others.
    - Wavelength Zone: Brings AWS services to the edge of a 5G network, reducing the latency to connect to you application from a mobile device.  Application traffic can reach application servers running in wavelength zones without leaving the mobile provider's network.
    - Outpost:  This is designed to support applications that need to remain in your datacenter due to low-latency requirements or local data processing needs.
    - Direct Connect Location:  This provides a direct connection to AWS using cross connections from other datacenters operated by the same providers used by AWS.

5.  Understand the purpose and function of as many AWS services as possible, starting with those listed in the exam guide
    -  This will be completed moving through the rest of the book