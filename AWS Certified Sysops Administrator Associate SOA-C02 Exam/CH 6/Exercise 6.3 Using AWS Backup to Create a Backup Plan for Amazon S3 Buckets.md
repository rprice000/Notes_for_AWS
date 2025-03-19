Exercise 6.3 Using AWS Backup to Create a Backup Plan for Amazon S3 Buckets


1. Go to AWS Backup Service
2. Click Create Backup Plan button
3. Select Build a New Plan
4. Type in a Name
5. Type in a Backup Rule Name
6. Backup Vault
    - Default
7. Select Backup frequency
    - Daily
8. Select Backup Window
    - Keep defaults
9. Life Cycle Policy
    - Keep defaults
10. Click Create Plan
11. Type Resource Assignment name
    - S3DemoBackup
12. Choose Default Role
13. Resource Selection choose either
    - Include all resource types
    - Include specific resource types
14. Click Assign Resources

15. On AWS Backup Dashboard click Create On-Demand Backup
16. Select Resource type
    - S3
    - Select bucket.  NOTE:  Bucket must have versioning enabled
17. Select Backup vault
18. Select IAM role
19. Click Create On-Demand Backup
