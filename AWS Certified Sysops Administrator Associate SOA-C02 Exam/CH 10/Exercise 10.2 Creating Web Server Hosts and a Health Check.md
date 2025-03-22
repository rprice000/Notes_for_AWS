Exercise 10.2 Creating Web Server Hosts and a Health Check

***NOTE: This exercise you will need a VPC Environment
- Create the VPC and more
- Security Group Inbound Rule
    - HTTP  0.0.0.0/0
- Security Group Outbound Rule
    - All traffic 0.0.0.0/0
- 2 EC2 Instances
    - Each in separate subnet
    - Enable Auto-Assign Public IP
    - Add the security group
    - Needs full SSM EC2 Role
Add the following script to the EC2 Instances
#!/bin/bash
yum update -y
yum install -y httpd.x86_64
systemctl start httpd.service
systemctl enable httpd.service
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
echo Route 53 Failover Test with WEB1 > /var/www/html/index.html

#!/bin/bash
yum update -y
yum install -y httpd.x86_64
systemctl start httpd.service
systemctl enable httpd.service
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
echo Route 53 Failover Test with WEB2 > /var/www/html/index.html



1. Go to the public ips of the EC2 instances in your web browser
2. Verifiy that both have the last command displayed
3. Go to Route 53 
4. On left hand side click Health Checks
5. Click Create Health Check button
6. Enter name
    - WEB1-HC
7. What to monitor
    - Endpoint
8. Under Monitor an Endpoint enter IP address of WEB1
9. Under Monitor an Endpoint path type index.html
10. Click Advanced Configuration
11. Select Fast (10 seconds)
12. Enter 2 for Failure threshold
13. Click Next button
14. Click Yes on Create Alarm
15. Select New SNS topic
16. Enter Topic Name: WEB1-HealthCheck
17. Enter Email: 
18. Click Create Health Check button

