CH 11

1. Remember that you are responsible for managing your app
    - Elastic Beanstalk is a managed service that simplifies the administration and deploymnet of web applications within AWS.  It takes advantage of CloudFormation to provision all the resources that you need to successfully run your web app.
    - Supports various languages and development stacks Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docket
    - Offers a range of features
        + Managed Platform Updates
        + CUstomization and Control
        + Automatic Scaling
        + Integrated Monitoring and Reporting
        + AWS Elastic Beanstalk CLI
        + Versioning and Life-Cycle Policies
    - Elastic BeanStalk has several layers with distinct roles
        + Application: Is a collection of different elements, including environments, environmnet configuration, and application version
        + Application Version: A unique reference to a section of deployable code
        + Environment: Refers to a deployed application version on AWS resources
        + Environment Tier: Determines how Elastic Beanstalk provisions resources based on what the application is designed to do.  Two main types of environment tiers
            ++ Web Server Tier: Standard applications that listen for and process HTTP requests typically over port 80.
            ++ Worker Tier: Specialized applications that perform background processing tasks and listen for messages in SQS queue.
    - Elastic Beanstalk provides several options for how deployments are processed
        + Single Instance:  Ideal for development. Application is deployed on a single instace
        + High Availability with Load Balancer:  Ideal fr production 
    - Five main deployment policies
        + All-at-Once:  New version is deployed to all instances simultaneously.  This policy is the fastest but involves a complete service outage during the deployment, making it unsuitable for mission critical systems
        + Rolling: Updates a few instances at a time, then moves onto the next batch once the first batch is healthy
        + Rolling with Additional Batch: Same as Rolling but launches new instances as a batch to ensure full availability.  The application will run both versions simultaneously
        + Immutable: Launches new instances in a new Auto Scaling Group and deploys the version update to these instances before swapping traffic to the instances once they are healthy
        + Blue/Green Deployment: Refers to using your application environmnet (Blue) and your staging environmnet (Green) side by side to test your new code with real production traffic

3. Understand what CloudFormation does
    - AWS CloudFormation lets you define and manage infrastructure using code.  Supports both YAML and JSON formats
    - Pricipal elements are templates and stacks.  A template is a JSON or YAML file that specifies the AWS resources you want to provision.  A stack represents the AWS resources defined by a template that have been provisioned 
    - CloudFormation's drift detection capability is a tool for maintaining the integrity of your stack resources

4. Rember what sections are in CloudFormation templates
    - AWSTemplateFormatVersion
        + Gives the template format version
    - Description
        + Describes what the template is for or what it does
    - Metadata
        + Adds more information about your template.  Used if you want to call out information specific to certain parts of your template
    - Parameters Intro
        + Gives you ability to add custom values to stacks using the same template
        + Four Types of Parameters
            ++ String
            ++ Number
            ++ List
            ++ Comma-delimited list
    - Pseudo Parameters
        + Used by CloudFormation to determine stacks using the same template
    - Mappings
        + Allow you to specifiy a key-value pair.  For each mapping a key must have a unique name, and keys are allowed to contain multiple values
    - Conditions
        + Used to determine whether a resouce should be created or whether a certain property should be assigned
    - Transform
        + Allows you to choose one or more macros for Cloudformation to use
    - Resources
        + Specifies the actual resources that you want to create, modify, or delete