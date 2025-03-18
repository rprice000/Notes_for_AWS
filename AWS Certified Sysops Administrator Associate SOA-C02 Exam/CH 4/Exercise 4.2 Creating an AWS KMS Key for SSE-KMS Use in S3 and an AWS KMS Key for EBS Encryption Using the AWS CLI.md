Exercise 4.2 Creating an AWS KMS Key for SSE-KMS Use in S3 and an AWS KMS Key for EBS Encryption Using the AWS CLI


1. Got to Key Management Service
2. Click Customer Managed Keys on left hand side
3. Click Create Key
4. Select Symmetric
5. Select Encrypt and decrypt
6. Click Next
7. Type in Alias
8. Type in Description (optional)
9. Add tags (optional)
10. Click Next Button
11. Select user who will be managing the account
12. Check Box Allow Key administrators to delete this key
13. Click Next
14. Set usage permissions (optional)
15. Click Next
16. Set Key policy (optional)
17. Review Selection
18. Click Finish Button



1. Open Terminal
2. Type in terminal
    - aws kms create-key --tags TagKey="Purpose",TagValue="EBS Encryption" --description "Encrypt EBS Volumes"
3. Type in terminal
    - aws kms create-alias --alias-name alias/ebsencryption --target-key-id <key-id>
4. Type in terminal
    - aws kms list-aliases --key-id <key-id>


