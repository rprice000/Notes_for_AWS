Exercise 8.7 Creating a Role for SSM and Attaching It to Your EC2 Instances


1. Go to IAM dashboard
2. On left hand side click Roles
3. Click Create Role
4. Click AWS service
5. Under Use case select
    - EC2
6. Click Next Button
7. Search for and check the box AmazonEC2RoleforSSM
8. Click Next Button
9. Give Role a name
10. Click Create Role

Attach to an EC2 Instance

15. Go to EC2 Dashboard
16. Click Instances
17. Check the box of the EC2 you want to add the role
18. Click Actions
19. Choose Security
20. Click Modify IAM role
21. Click the down down arrow and select the role you created