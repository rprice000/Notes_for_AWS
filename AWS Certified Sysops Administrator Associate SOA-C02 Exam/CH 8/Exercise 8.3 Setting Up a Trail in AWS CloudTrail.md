Exercise 8.2 Setting Up a Trail in AWS CloudTrail


1. Go to CloudTrail Service
2. Click Create a trail button
3. Type Name of Trail
4. Uncheck Enable for all accounts in my organization
5. Uncheck Boxes
    - Log File SSE-KMS Encryption
    - Log File Validation
    - SNS Notification Delivery
    - CloudWatch Logs
6. Click Next Button
7. Under Events Check the box for
    - Management Events
    - Data Events
8. Under Management Events Check the box for
    - Read
    - Write
9. Under Data Events click Switch to basic event selectors
10. Click Continue
11. Data Event Source: S3
12. All current and future S3 buckets check the box for
    - Read
    - Write
13. Click Add data eventy type button
14. Under Data Event Select Lambda
15. Select All Regions
16. Click Next Button
17. Review the selections
18. Click Create Trail
