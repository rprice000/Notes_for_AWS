Exercise 4.4  Creating and Storing Credentials in Secrets Manager

1. Open Secrets Manager in Console
2. Click Store a New Secret
3. Select the Type of Secret
    - Other type of secret
4. Select either
    - Key/Value
    - Plaintext
**Note: in this scenario we chose Key/Value
5. Add Key/Values
    - Key: Username     Value: DemoSecret
    - Key: Password     Value: password
6. Select Encryption Key
    - Default:  aws/secretsmanager   NOTE:  This will generate a new key.
    - Your own key already in KMS
7. Click Next
8. Type in Name of Secret
9. (Optional) Type in Description
10. (Optional) Type in Tags
11. Click Next Button
12. (Optional) Configure secret rotation schedule  ***NOTE: In real life you will have to configure a rotation schedule
13. Click Next Button
14. Review selection
15. Click Store

16. Open CLI
17. Type in
    - aws secretsmanager list-secrets
18. See the Name of the secret
19. Type in
    - aws secretsmanager get-secret-value --secret-id <SECRETNAME>