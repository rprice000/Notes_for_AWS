CH 2 Account Creation, Security, and Compliance

Exam Essentials

1.  Know the Shared Responsibility Model
    - The customer and AWS each have a role to play securing a cloud computing environment and its resources.
    - AWS is responsible for security of the cloud and the customer is responsible for security in the cloud.
    - AWS is responsible for the inherited controls, which include the physical and logical infrastructure that the customer's environment runs on.
    - There is a shifting line of responbility, which moves up as the dregree of abstraction increases for the service.  By absraction, we mean that AWS takes on more responsiblity  and there is less for the customer to manage.
    - Customer Responbility
        + Encryption
        + Network Traffic Protection
        + OS
        + Network Config
        + Firewalls
        + Identitiy Access Management
        + Application and Platform Security
        + Customer Data
    - AWS Responsiblity
        + Foundational Serivces
            ++ Compute, Storage, Databases, Networks
        + AWS Infrastructure
            ++ Data Centers, Regions, Edge Locations, Availability Zones

2.  Recognize that everything is an API
    - AWS Organizations provides for the central management of accounts with a single bill payer, centralized policies, monitoring, and resource proisioning
    - AWS Organizations enables the following
        + Automated account creation and management
        + Automated resource provisioning
        + Improved security by creating and enforcing structure
        + Reduced management overhead
        + Simplified auditing for compliance
        + Centralized billing
        + Simplified AWS service configuration accross accounts
    - There is no cost for AWS Organizations.  You only pay for the resources created in the accounts
    - Inside Organizations you can have organizational units (OUs) which is a logical container for accounts
    - SCPs can be attached to OUs
    - A service control policy is similar to a permissions boundary in that if defines the limits of permissions that could be granted.  An SCP does not grant permissions.
    - SCPs do not apply to users or roles in the management account, only to member accounts in an organization.
    - AWS Control Tower works with AWS Organizations to provide additional features to manage authentication and authroization
    - Control Tower comes with:
        + Landing Zone
        + Guardrails
        + Account Factory
        + Dashboard
    - A landing zone is a well-architected, multi-account environment.  There can only be one landing zone.
    - Guardrails are high-level rules for the organization.  They allow you to implement preventive and detective controls on a given OU and all OUs below.  All guardrails have a behavior and a guidance.
    - Preventitive guardrails are implmeneted as service control policies from AWS Organizations.  Detective guardrails are implemented using AWS Config rules
    - Guardrail's guidance determines the enforcement of the guardrail. Guidance is either mandatory, strongly recommended, or elective.
    - Guardrails with a detective behavior use AWS Config and are in one of three states: clear, in violation, and not enabled.  Detective Guradrails are only available in regions where AWS Control Tower is supported.  SCPs from AWS Organizations are used for preventitive guardrails and are either enforced or not enabled.  Preventitive guardrails are available in all AWS regions.

3.  Remember Authentication vs Authorization
    - Authentication is being sure the actor is who they say they are.
        + We authenticate in three ways:
            ++ usernames/password (what we know)
            ++ fingerprint or facial recognition (who we are)
            ++ token or smartcard (what we have)
    - Authorization defines what we can do once we are authenticated
    - IAM is used for both
    - IAM is a suite of tools for managing authentication and authorization
    - Every request for access to any AWS resource passes through IAM.  Each request made to IAM there is context.  The context is taken into account when determining permissions.  The context may include data in the request itself or data gathered throgh the process of making the request.
    - The Context can include the following:
        + What actions are being requested
        + What resources will be accessed
        + Who is making the request
        + Where and When
        + What specific resource
    - The attributes of the context then become vital data for how IAM policies determine access using attribute-based access control
    - Attribute Based Access Control (ABAC) is a model for granting permissions in IAM.  It is much more granular and allows the same user to have different permissions in different context.

4.  Know Directory Services Use Cases
    - AWS Directory Services come in three flavors
        + AWS Active Directory Services for Microsoft Active Directory
        + AD Connector and AWS Active Directory Service are both using Microsoft Active Directory and will have similar functionality and prerequisites.  Simple AD is Microsoft AD compatible, it runs on Samba 4 and locks advanced features like SSO and MFA
        + AWS Active Directory Service for Microsoft Active Directory is a fully managed service users have no access to the instance it runs on.
            ++ It comes in two editions
                +++ Standard:  Used for organizations with up to 5,000 employees and 30,000 directory objects
                +++ Enterprise: Used for organization with up to 500,000 directory objects
            ++ No additional Client Access License the CAL is included in the service pricing.  You are build at an hourly rate
        + AD Connector connects to an on-premises Active Directory.  It creates a trust relationship between AD and specific AWS services.
            ++ AD Connector has a limited set of capabilities
                +++ Allow federated sign-in to the AWS console
                +++ Allow federated users access to services
                +++ Join Windows EC2 instances and S3 bandwidth to AD domain
                +++ Integrate with Radius server to enable MFA
                +++ Enforce IAM security policies against resources joined to AD Connector
            ++ AD Connector does not store the directory data.  It only connects AWS to the authoritative AD store
            ++ AD Connector does not integrate with RDS SQL server
            ++ AD Connector pricing is based on the directory size:  large or small
        + Simple AD is a directory store rather than just a connector.  It is a fully managed service built on a Samba 4 AD-compatible server and is best used for cases that have a limited number of users (under 5,000) and the complexities of Microsoft AD are not needed.

5. Know IAM policies
    - There are several policy types.  Some grant permissions others limit access.
    - Policies can be thought of as identity-based or resource-based.  The difference between them is where the policy is attached.  Identity-based policies are associated with the user and travel with the user.  Resource-based policies are associated with the resource rather than with the user and the user comes to the resource for access.
    - Identity based policies apply to users, groups, and roles
    - Resource based policies apply to resources
    - Permission boundaries apply to identity based policies and define the limits of what an entity can do.  They limit and do not grant permissions.
    - Service Control Policies apply to all identities and resources within an account and limits what they can do but cannot grant permissions
    - Access Control Lists (ACLs) apply to principles in other accounts.  Cannot be used with entities in the same account.
    - Session Policies are used with requests through the CLI or APIs when assuming a role or with a federated user.  Session Policies are used to limit not grant, permissions
    - IAM Policies have 3 components
        + Effect
        + Actions 
        + Resource
    - Policies also have optional conditions. Policies also can use variables, wildcards, and tags to expand policy capabilities to provide granular control
    - A Role consists of two parts
        + A trust policy which determines who can use the role
        + A permission policy which descrives what the entity can do
    - A Role is used to grant fine grained access and to delegate access.  Roles are like temporary permissions to do a specific action.
    - NOTE:  If there is no explicit allow, access is denied even if there is no explicit deny

6. Understand Common IAM Tasks
    - Root User best practices:
        + Use root user account only when necessary
        + Never assign security keys to the root user
        + Apply 2-Factor authentication
    - IAM users will have usernames and passwords
        + They are also assigned password for console access and/or access keys for programmatic access
    - One password policy applies to the entire account, and each account can have only one policy.  The default policy is eight characters in length, a combination of four character types, and cannot be your account or email address.  Password length and complexity, expiration, require administrator requests
    - Credential Reports can be run to collect info on IAM users
        + Fields include:
            ++ If MFA is enabled
            ++ Password next rotation
            ++ If access key is Active
            ++ Last used data
    - IAM Access Analyzer determines if someone can access your resources.  It helps admins determine what resources are shared outside of their zone of trust, either as an organization or for an account.
    - The zone of trust can be your organization or your account
    - IAM Analyzer monitors:
        + S3 Buckets
        + IAM Roles
        + Key Management Service
        + Lambda functions and layers
        + Simple Queue Service
        + Secrets Manager
    - You can also validate policies using policy checks in Access Analyzer.  These policy checks evaluate your policy for grammar and best practices.  You can generate policies using Access Anaylzer to align your policies to real usage.
    - IAM Policy Simulator is used to test identity based and resource based policies including the implications of permissions boundaries and SCPs if the account is a member of AWS Organizations. The policy simulator allows testing of policy conditions with the exception of global condition keys in AWS Organization SCPs.