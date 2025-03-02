CH 9 Networking

1. Common CIDR ranges
    - Three ranges
        + 10.0.0.0 - 10.255.255.255
        + 172.16.0.0 - 172.16.255.255
        + 192.168.0.0 - 192.168.255.255
    - 10.255.255.255 can be written as 10.0.0.0/16 which contains 65,536 addresses
    - 10.0.0.0/28 has 16 addresses
    - /16 is the largest range and /28 is the smallest range

2. How to create an Elastic IP address and attach to an EC2 instance
    - An Elastic IP (EIP) is a static, public IPv4 address that you can allocate and manage within AWS.  It allows you to maintain a consistent IP address even if you stop and restart an EC2 instance
    - Key Features
        + Static Public IP
        + Reassociation:  Able to reassign the IP if needed
    - Can be assigned in the EC2 dashboard of a specific instance

3. Know your Gateways and Connectivity
    - Internet Gateway
        + Used to connect VPC resources to the public internet.  IGWs are hgihly available and scalable and handle all traffic on all ports
        + An IGW can be attached to or detached from a VPC
    - Egress-Only Internet Gateway
        + Similar to IGW but has no configuration
        + Only has IPv6 traffic pass through
        + To allow only IPv6 to pass through a NAT Gateway or EIGW must be in place
        + EIGWs are stateful, meaning that when traffic is sent from the VPC, responding traffic is returned to the initiatin resource
        + The EIGW is not attached to or detached from the VPC 
    - DirectConnect
        + A common enterprise datacenter connection to a VPC. Provides a dedicated connection at speeds from 50 Mbps to 100 Gbps
        + Requires working with a DirectConnect delivery partner and takes time to get up and running
        + This is a big network pipe, however it is a single point of failure
    - VPN
        + There are several forms of VPN used to connect from on-premises to the VPC
        + Simplest is an IPSec VPN over the Internet with a customer gateway on the customer side and a Virtual Private Gateway on the VPC side. This requires the assignment of a Border Gateway Protocol (BGP) Autonomous System Number (ASN) either on their own or through AWS
    - Transit Gateway
        + Can connect multiple VPCs and acts as a central connection point for all network traffic coming into your environment.  Costs include a fee per attachment and data processing
    - VPC to VPC and Services
        + A logically isolated virtual network analogous to an on-premises datacenter.  DirectConnect or a VPN can be used to connect on-premises resources to the VPC to form a hybrid network.  VPC peering and VPC endpoints can be used to expand your network to additional VPCs and to many other AWS services

4. Understand how to monitor your network
    - Traffic Mirroring
        + Allows you to copy inbound and outbound network traffic at an ENI to a security monitoring device
        + A traffic mirroring source is an ENI, network load balancer, or gateway load balancer.  The destination is where the mirrored traffic is sent.  Filters are rules to determine what traffic is sent.  A session combines the source, the destination, the target, and the filters
        + Uses port UDP 4789 (VXLAN)
    - Reachability Analyzer
        + Tool used to diagnosis IPv4 network connectivity issues
        + Used to identify issues with security groups, route tables, and NACLs configurations
    - VPC Flow Logs
        + Captures information about traffic on network interfaces in the VPC, including those attached to EC2, ELB, RDS, ElatiCache, etc.
        + Can be created from a variety of consoles, including Network Interfaces in EC2 console
    - Elatic Load Balancer Logs
        + Can publish logs for each node every 5 minutes. Logs contain time of request, client IP, latency, request path and server response
    - Web ACL Traffic Logs
        + Service allows the logs to be sent to a CloudWatch log group, Kinesis Fire HOse, or S3 and is billed for storage in the destination service
        + Will show information about the time stamp and details of the request, and which WAF rules were matched.