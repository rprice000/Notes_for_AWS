CH 3

1. Understand the importance of implementing AWS Cost allocation tags
    - Cost allocation tags enable organization of resources on the cost allocation report to make it easier for an administrator or organization to categorize or track AWS costs.  There are two distinct types of cost allocation tags:  AWS generated tags and user-defined tags.  AWS generated tags are automatically defined, created, and applied, whereas user-defined tags must be manually defined based on the organization's needs and then applid to the AWS Cost Explorer or cost allocation report.  You must activate both types of tags separately before then can appear in each report.
    - User cost allocation tags should represent categories that are meaningful to project or business function.
    - User-defined tags can take up to 24 hours to appear in the AWS Billing and Cost Management console.
    - Cost allocation tags appear on the console after you have enabled Cost Explorer, Budgets, or AWS Cost and Usage Reports.

2. Understand how to export AWS Cost and Usage Reports
    - Cost and Usage Reports, up to 10 per account, or AWS Data Exports up to 5 per account, are placed in an S3 bucket for review.  Each update across any month is cumulative.
    - Any report data provided throughout the month is just an estimate of your AWS services being used, which means these estimates can change based on how you continue to use the services.
    - It is important to remember that the report may change if you AWS account has any pending refunds or credits or the account support fees change based on your usage for that month.  You can tell if your AWS Cost and Usage Report is finalized by looking for the Bill/Invoice ID column in your CSV file.  If that column is present, the bill has been finalized and will not change.
    - If at any time you want to analyze or download your AWS Cost and Usage Reports you can open the Amazon S3 Console and download the CSV file from your Amazon S3 Bucket.  You can also query the reports using Amazon Athena directly from the S3 Bucket or upload the reports into Amazon Redshift or Amazon QuickSight for further analysis.

3. Understand how to create AWS Budget notifications and actions
    - AWS Budgets is used to enable cost and usage tracking within an AWS account and act on any monitored area.  AWS Budgets can aggregate and act on any monitored area.  AWS Budgets can agregate utilization and coverage metrics for Savings Plans and Reserved Instances (RIs), which provides a unified location to evaluate cost-saving mechanisms applied against your AWS accounts.
    - Six budget types are available within AWS Budgets:
        + Cost Budgets
        + Usage Budgets
        + RI Utilization Budgets
        + RI Coverage Budgets
        + Savings Plan Utilization Budgets
    - Each budget type can set up an optional notification based on thresholds configued within the budget.
    - Budget alerts use Amazon SNS to send notifications and have a one-to-one ratio of Amazon SNS topics to alerts.  An AWS Budget alert can also be sent to up to 10 email addresses in addition to the Amazon SNS topic, which offers expanded options in providing automated actions or advanced notification options like SMS text messaging or AWS Lambda event triggers.
    - The frequency of notifications depends on the alarm type and event.  Actual Budget alerts send out once per budget, per period, and only when the first threshold breaches, whereas forecast-based alarms may send out notifications more than once if the budget exceeds the alarm threshold and then goes below.  If the budget forecast looks to exceed the threshold again another alarm trigger will occur.
    - AWS requires five weeks of usage data before it can generate budget forecasts.

4. Understand how to identify and remediate unused resources usng AWS Cost Explorer
    - AWS Cost Explorer enables both high-level and detailed analysis of cost and usage usin several filtering dimensions, such as region, AWS service, and cost allocation tags.
    - AWS Cost Explorer is handled using the Billing and Cost Management console.  The account status within an organization can affect what cost and usage data is available and a management account can block access to member accounts within Cost Explorer.
    - Cost Explorer provides several preconfigured views to display information about your cost and usage trends.  You can use Cost Explorer to view a quick visualization of the top five cost-accuring AWS services or an analysis of the overall Amazon EC2 usage within a specific account.
    - Cost Explorer is also extremely helpful in visualization of the Reserved Instance Utilization auditing, planning, and evaluating current reservations.  Cost Explorer prepares data for the current month and the last 12 months and even allows forcasting for the next 12 months.
    - You can create up to 50 custom reports to suit the needs.  If you want to programmatically access your data using the Cost Explorer API, you will incur a charge of $0.01 for each paginated API request.

5. Understanding AWS Managed service opportunities to reduce cost
    - A cost reduction that is often overlooked is the cost it takes for IT administrators to manage an environment.  When you can make a reduction in scope of work due to managed services, this enables an intangible cost savings for the organization.  When an administrator isnt focused on just keeping the lights on, they can focus on automation, backups, future cost optimization tasks, and security of the AWS Account.
    - You may be thinking to yourself that IT administration overhead doesn't really account for much in the organization.  You have administrators handling 50-75 servers currently.  If they had more native monitoring, automation tools, and visibility; a conservative estimate of the numbe of servers that a single admin could manage may be 150-200.
    - The number may not go up or down but administrative time would lessen.  Giving admins more time for other tasks.

6. Understand when to use Savings Plans
    - Savings Plans is a pricing model used to provide savings of up to 72% on AWS compute workloads.  Savings Plans require a commitment of using an agreed-on amount of compute power, measured by the hour, over a one or three year period.  You can pay using No Upfront, Partial Upfront, and All Upfront.  There are three different types of Savings Plans
        + Compute Savings Plans
            ++ The Compute Savings Plans target flexilbility and pricing, which offer up to 66% off normal On-Demand rates.  This plan removes the regional and instance type limitations.  The plan also applies across EC2 instance usage no matter what the instance family.  This plan is not exclusive to any OS.
        + EC2 Instance Savings Plan
            ++ If you are using specific instance families in a specific region. This plan may offer up to 72% off On-Demand pricing.  This plan allows for changes to instance size or OS within the specific family.
        + Sagemaker Savings Plan
            ++ This plan is for heavy Sagemaker use. It can provide up to 64% off On-Demand rates.  It helps with Sagemaker notebook or training.  It has the ability to move workloads between regions or migrate usage between Inference or Training at any time.
        + Savings Plans vs. Reserved Instances
            ++ Savings Plans are more flexible than RIs as you can commit to usage on a per hour basis, rather than committing to a specific instance configuration.  RIs would require a manual exchanging or modifying of the agreement to achieve a similar result, but only when using convertible RIs.
        + Savings Plans are pricing models only and do not guarantee or provide capacity to achieve reservations for On-Demand instances, you will need to allocate On-Demand Capcity Reservations (ODCR) in addition to configuring the Savings Plans.  Savings Plans also do not apply to spot instance usage or any usage covered by a RI.  This means that you cannot stack discounts to achieve an even larger discount.
        + Monitoring Savings Plans
            ++ Savings Plans have four different methods for evaluating and monitoring usage:  Inventory, Initialization Report, Coverage Report, and Budgets
                +++ Monitoring Using Inventory
                    ++++ The Monitoring option provides an overview of any Savings Plans currently owned or queued for future purchase in the AWS account. The inventory provides detailed information about the Savings Plan, such as type, instance family, region, month-to-date net savings, states, and dates.  It gives you the ability to download the Savings Plan rates and Savings Plans Inventory.
                +++ Monitoring Using Utilization Reports
                    ++++ A utilization report provides a visual representation of how the Savings Plans commitment apply to AWS account On-Demand usage over a specified time period.  The utilization report also provides a quick glance at several useful metrics and filters to make useful renewal decisions or modifications to the Savings Plans based on new business needs or project changes.
                    ++++ All utilization is calculated across a period called a loopback period.  The loopback period is basically a start and an end date where the visualization and utilization reports are evaluating.  This loopback period is what the high-level metrics use to provide utilization details, spend details, and net savings.  The utilization report offers metrics for evaluation in the categories of On-Demand Spend Equivalent, Savings Plans Spend, and Total Net Savings.
            ++ Monitoring Using Coverage Reports
                +++ If you want to determine how much spend was covered by the purchased Savings Plans, the coverage report is the place to look.  The coverage report can be reviewed for a specific time period.  The coverage report includes three high-level metrics
                    ++++ Average Coverage metric:  Shows an aggregated coverage percentage based on the loop back period selected
                    ++++ Additional Potential Savings Metric:  Shown as a monthly amount, supports reviewing the amount saved by Savings Plans recommendations
                    ++++ On-Demand Spend Not Covered Metric: Shows the amount of savings spend that was not covered by a Savings Plan or Reserved Instance Purchase.
