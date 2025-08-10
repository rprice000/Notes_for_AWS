 Deployment Steps in the AWS Console:
1. Log into the AWS Console
Navigate to: https://console.aws.amazon.com/

Make sure you are in the Commercial partition, not GovCloud.

2. Open CloudFormation
In the top search bar, type CloudFormation

Click on CloudFormation to open the console

3. Create a New Stack
Click “Create stack”

Choose “With new resources (standard)”

4. Upload the Template
Under Specify template, choose:
✅ “Upload a template file”

Click “Choose file” and select your corrected proserve-assume-role-admin.yaml from your computer

Click Next

5. Stack Details
Stack name: Enter
proserve-administrator-role

Leave everything else as-is

Click Next

6. Configure Stack Options
You can skip this section (leave defaults)

Click Next

7. Acknowledge IAM Resource Creation
Scroll to the bottom

Check the box:
✅ “I acknowledge that AWS CloudFormation might create IAM resources with custom names.”

Click Submit / Create stack

8. Monitor the Stack Deployment
You'll be taken to the Stack details page

Watch the Status column

It will show CREATE_IN_PROGRESS

Wait until it becomes CREATE_COMPLETE (this usually takes <1 minute)

✅ After the Stack Completes
The following resources will now exist in your Commercial management account:

IAM Role: proserve-administrator-role

IAM Policy: deny-all-policy

The role will:

Be assumable by AWS ProServe (account 676486052569)

Be granted AdministratorAccess

Automatically lose access after 2025-10-31 due to the deny-all policy




https://docs.aws.amazon.com/solutions/latest/landing-zone-accelerator-on-aws/option-2-deploy-on-new-aws-govcloud-us-accounts.html