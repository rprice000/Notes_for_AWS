Exercise 1.4 Provisioning Admin Users with IAM


How to Create a User Group

1. Login as Root User
2. Go to IAM Landing page
3. On right hand side make note of Account ID and Alias     
    277910805011/reagan-aws-mk1
4. On right hand side make note of the sign-in URL for non-root accounts. URL should have either alias or account id in the URL     
    https://reagan-aws-mk1.signin.aws.amazon.com/console
4. On left-hand side select Access Management > User Groups
5. Right-hand side click Create Group Button
6. Type in name of Group
    Administrators
7. In the section Attach permissions Policies locate search bar search for Administrator
    NOTE:  You can attach up to 10 policies to a User Group
8. Check the box for AdministratorAccess
9. Bottom right click Create User Group


How to create a User

1. Login as Root User
2. Go to IAM Landing page
3. On left-hand side select Access Management > User
4. On top right hand side click Create User Button
5. Type in name
6. If you want user to have CLI access then Check the Box
    - Provide user access to the AWS Management Console - optional
7. Click Next Button
8. Select Add user to group
9. Check Box to the group the user should be in
    - Administrator
10. Click Next Button
11. Click Add new Tag
    - Enter Key
    - Enter Value
12. Click Create User