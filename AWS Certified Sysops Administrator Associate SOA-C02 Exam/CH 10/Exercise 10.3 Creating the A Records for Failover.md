Exercise 10.3 Creating the A Records for Failover

***NOTE: This is a continuation of 10.1 and 10.2


1. Go to Route 53 Dashboard
2. On left hand side select Hosted Zones
3. Select the hosted zone you created in 10.1
4. Click Create Record button
5. Enter in Record domain
    - www
6. Select under Record Type
    - A-Routes traffic to an IPv4 address and some AWS resources
7. Enter in Value the IP of first instance
8. Under Routing Policy select
    - Failover
9. Under Failover Record Type select
    - Primary
10. Under Health Check ID choose the Health Check you created in 10.2
11. Enter a Record ID
***NOTE: This will be an ID you make up
12. Click Create Records button

You will do the same for the second instance
13. Click Create Record button
14. Enter in Record domain
    - www
15. Select under Record Type
    - A-Routes traffic to an IPv4 address and some AWS resources
16. Enter in Value the IP of first instance
17. Under Routing Policy select
    - Failover
18. Under Failover Record Type select
    - Primary
19. Under Health Check ID choose the Health Check you created in 10.2
20. Enter a Record ID
***NOTE: This will be an ID you make up
21. Click Create Records button