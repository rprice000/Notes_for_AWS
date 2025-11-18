Exam Essentials


1. Understand AWS platform architecture
    - AWS maintains datacenters for its physical servers around the world.  Because the centers are so widely distributed, you can reduce your own servers' network transfer latency by hosting your workloads geographically close to your users.  It can help you manage compliance with regulations, requiring you to keep data within a particular legal jurisdiction.
    - Datacenters exist within AWS regions, of which there are currently 21 - not including private U.S. government AWS GovCloud regions - although this number is constantly growing.  It's important to always be conscious of the region you have selected when you launch new AWS resources; pricing and service availability can vary from one to the next.
    - Because low-latency access is so important, certain AWS services offered from designated edge network locations.  These serices include Cloudfront, Route 53, Firewall Manager, Shield, and WAF
    - Physical AWS data centers are exposed within your AWS account as availability zones.  There might be half a dozen availability zones within a region each consisting of one or more datacenters
    - You organize your resources from a region within one or more virtual private cloud (VPCs). A VPC is effectively a network address space within which you can create network subnets and associate them with availability zones.

2. Understand how to use AWS administration tools
    - Though you will use your browser to access the AWS administration console at least from time to time, most of your serious work will probably happen through the AWS CLI and, from within your application code, through an AWS SDK.
    - If you want to incorporate access to your AWS resources into your application code, you'll need to use an AWS SDK for the language you're working with AWS currently offers SDKs for nine languages.
    - The AWS command line interface CLI lets you run complex AWS operations from your local command line.

3. Know how to choose a support plan
   - Basic Support Plan
     - This plan is free with every account and gives you access to customer service, along with documentation, whitepapers, and the support forum. Customer service covers billing and account support issues.
   - Developer Support Plan
     - This plan starts at $29/month or 3% of monthly AWS Charges and adds access for one account holder to a Cloud Support associate along with limited general guidance and "system impaired" response.
   - Business Support Plan
     - Thi plan starts at $100/month or 10% of monthly AWS charges up to $10,000.  This plan will deliver faster guaranteed response times to unlimited users for help with "impaired" systems, personal guidance and troubleshooting, and a support API.
   - Enterprise On-Ramp
     - This plan starts at $5,500 or 10% of monthly AWS charges.  This adds fast response for business critical system down events and proactive guidance and consultative review based on your applications.
   - Enterprise 
     - This plan covers all of the other features plus direct access to AWS solutions architects for operational and design reviews, your own technical account manager, and access to online self paced labs.  This plan costs $15,000 a month

4. Understand how to migrate existing applications and resources to AWS
   - Migratin Hub
     - This service helps organizations track their progress as they migrate their workloads to the AWS cloud.  It provides a dashboard as a central place to view information about your existing inventory and the status of all your migration projects, making it easy to track progress and identity and issues.
     - It can be used to coordinate the operations of all migration-related AWS tools and to assess the feasibility of migrating your workloads to AWS.  It can also help transform and refactor your specific workloads as cloud-native applications
   - Application Migration Service
     - Is a tool that automates the testing and transfer of AWS-bound migrations of your non-cloud application servers
     - Start by installing the Replication Agent of each of the servers you want migrated. The agents will initiate replication in the background without impacting your ongoing server operations.  Once your application software has reached the cloud, the service will test everything to ensure it's fully operational.  Once thats confirmed, the final seamless cutover will be executed and your application will launch on AWS.
   - Database Migration Service
     - Has the same basic goals as Application Migration Service but for databases.  The idea is to make your non-cloud data available to your applications in the cloud with comparable or better performance.  Instead of installing Replications Agents, all you need to provide is access, along with your existing database endpoints.
     - You can create what they call a homogenous migration (Oracle-to-Oracle, MariaDB-to-MariaDB). But you also could convert a relational database to a data lake that lives in S3, or move Oracle database to Amazon Aurora.
   - Application Discovery Service
     - Helps you plan application migration projects by identifing which applications are running in your on-premises datacenter, how they are interconnected, and how they use your resources.
     - This service inventories your datacenters, collects information about your applications, and then creates a configuration model of your applications and their dependencies.
     - To use the service you'll need to install Application Discovery Service Discovery Agents on your on-prem servers.  The agents will then get to work gathering data about those resources and their dependencies.  Data collected by Application Discovery Service is retained in a data store.  You can optionally export this data inta a CSV file for your own planning and records.