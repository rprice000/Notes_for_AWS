Exercise 6.2 Creating a Snapshot Lifecycle Policy


1. Go to EC2 Service
2. On left hand side under Elastic Block Store select Lifecycle Manager
3. Select EBS snapshot policy from drop down menu
4. Click Next Step button
5. Select Volume under target resource types
6. Enter Key/Value Pair
    - Key: Dev
    - Value: Finance
7. Enter a Policy Description
    - Development Finance Backup
8. Under Policy status click Enabled
9. Click Next Button
10. Configure Schedule Details
    - Frequency: Daily
    - Every: 12 hours
    - Starting at: 6:00 UTC
    - Retention Type: Age  Expire from standard tier: 2  days
11. Click Review Policy Button
12. Review Selection
13. Click Create Policy button


14.  When you create a EBS Snapshot you will add the Tags of the key/value pair from this Lifecycle Manager Rule