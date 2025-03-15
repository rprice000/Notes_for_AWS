Hands On Exercise 1.1: Creating an Amazon VPC with a Public Subnet Using AWS CloudShell

1. Open CLI in the AWS Console
2. Provision a new VPC using CIDR of 10.180.0./16
    aws ec2 create-vpc --cidr-block 10.180.0.0/16 --output text --query 'Vpc.VPcId'
3. Notate the VPC ID that is returned
    vpc-0fbf21d5550493965
4. Provision Tags for the VPC
    aw ec2 create-tags --resources vpc-0fbf21d5550493965 --tags Key=vpcname,Value=MyTestVPC
5. Provision an Internet Gateway
    aws ec2 create-internet-gateway --output text --query 'InternetGateway.InternetGatewayId'
6. Notate the Internet Gateway ID
    igw-0a500c14869869d02
7. Attach the Internet Gateway to the VPC
    aws ec2 attach-internet-gateway --internet-gateway-id igw-0a500c14869869d02 --vpc-id vpc-0fbf21d5550493965
8. Provision a subnet with a CIDR of 10.180.1.0./24
    aws ec2 create-subnet --vpc-id vpc-0fbf21d5550493965 --cidr-block 10.180.1.0./24 --availability-zone us-east-1a --output text --query 'Subnet.SubnetId'
9. Notate the Subnet ID
    subnet-0747b02d0bb936811
10. Provision tags for the public subnet
    aws ec2 create-tags --resources subnet-0747b02d0bb936811 --tags Key=subnet,Value=PublicSubnet
11. Obtain Route ID associated with the new VPC
    aws ec2 describe-route-tables --filters Name=vpc-id,Value=vpc-0fbf21d5550493965 --output text --quey 'RouteTables[*].RouteTableId'
12. Notate the Route Table ID
    rtb-008f73396f0e4baa8
13. Provision a route table entry for public Internet Access
    aws ec2 create-route --route-table-id rtb-008f73396f0e4baa8 --gateway-id igw-0a500c14869869d02 --destination-cidr-block 0.0.0.0/0
14. Associate the route table to the subnet 
    aws ec2 associate-route-table --subnet-id subnet-0747b02d0bb936811 --route-table-id rtb-008f73396f0e4baa8