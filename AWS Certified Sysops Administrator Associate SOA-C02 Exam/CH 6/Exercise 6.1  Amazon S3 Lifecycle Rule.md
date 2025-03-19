Exercise 6.1  Amazon S3 Lifecycle Rule

1. Go to S3 Service
2. Create a new S3 Bucket
3. Create 3 files on your desktop as a test
4. Upload the documents to the new S3 Bucket
5. Pick 2 documents Edit the tags
    - Key: Project
    - Value: Demo
6. From S3 Dashboard select the S3 Bucket you just created
7. Click Management Tab
8. Click Create Lifecycle Rule button
9. Type in a Name
10. Click Add tag button
11. Under Lifecyle rule actions
    - Select an action
    - Transition current versions of objects between storage classes
12. Choose storage class transitions
    - Standard-IA
    - 30 Days
13. Click Create Rule