CH 10

1. Understand how DNS works
    - The Domain Name System (DNS) provides a method to translate between human-readable addresses and the IP addresses that systems use to communicate over IP-based networks.
    - Going to a specific site your system will reach out to its local DNS server with a DNS query to see if the local DNS knows the IP address for the site.  If it knows the answer the local DNS will respond with the IP.  If it doesn't it sends the query to a top-level domain DNS server.  The TLD will respond with the address of the authoritative DNS server for the site.  DNS operates over the network using TCP and UDP over port 53.  UDP was historically used for DNS but large network packets if IPv6 and/or DNS Security signed records use TCP.  It is also used for zone transfers, the process of propagating name-to-IP address records between servers.

2. Know the various DNS record types
    - A: The A record is used to map a hostname to an IPv4 address
    - AAAA: The AAAA record is used to map a hostname to an IPv6 address
    - PTR: A pointer (PTR) record is used to do reverse DNS lookups
    - CNAME: A canonical name (CNAME) is used to create a "nickname" to a true and actual name.  Commonly used in web hosting to map a name like www.website.com to the actual name of the server that hosts the website.  The actual name of the server can be something.website.com but publicly it can also reached using www.website.com.  PLease note that DNS does not allow the creation of a CNAME record to top node of a DNS name.  You cannot create a CNAME for website.com by itself.
    - SOA: The start of authority (SOA) record is used to define the authoritative DNS servers for an individual DNS zone
    - NS: Name Serer records are used to identify the DNS servers for a given hosted zone.
    - TXT: The text record is used to provide information in a text format systems outside of your domain.
    - MX: Mail exchange records are used to identify email servers for a given domain.  They can also be used to set the priority of the email servers if there are multiple hosts behaving as email servers.
    - CAA: A CAA record is used to identify vaid certificate authorities from being used to issue certificates for your domain.
    - NARTP: Used to "chain" multiple records together to create rewrite rules, which can create things like uniform resources identifiers (URIs) or domain labels.  Also needed in the context of Dynamic Delegation Discovery System (DDDS) applications
    - SPF: The Sender Policy Framework is used to identify the sender of email messages and validate that the identity presented is true.  The use of SPF is not recommended by AWS
    - SRV: The service record is used to identify hostnames and port numbers for servers that provide services with a DNS zone

3. Understand what Routing Policies do
    - Simple Routing
        + Used when you need to route traffic without any special conditions.  Allows you to apply more than one IP address to a record, but the results are returned in a random order
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
    - Weighted Routing
        + Used when doing blue/green deployment to test new versions of software.  Route 53 will create a sum of weights for all the records being used and responds to queries based on a ratio of a resource's weight to the total sum.
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
            ++ Weight
            ++ Health Check ID
            ++ Record ID
    - Geolocation Routing
        + Used to decide where users will be directed based on their location
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
            ++ Location
            ++ Health Check ID
            ++ Record ID
    - Latency Routing
        + Used to direct users to a region that can provide the lowest latency.  The region with the best latency may not be the region that is closest to the end user.
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
            ++ Region
            ++ Health Check ID
            ++ Record ID
    - Failover Routing
        + Used to direct traffic to a primary instance while it's healthy but divert traffic to a secondary instance if the primary becomes unhealthy
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
            ++ Failover Record Type
            ++ Health Check ID
            ++ Record ID
    - Multivalue Answer Routing
        + Used to return multiple values (IP addresses) in response to a query.  Can be assured the IP addresses being returned are from  healthy hosts, since it can do health checks if you set it to
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
            ++ Value/Record Traffic to
            ++ Health Check ID
            ++ Record ID
    - IP-Based Routing
        + Enables you to route traffic to resources in your domain based on the client subnet ID.  This is useful if you want to optimize network transit costs to route end users from a particular ISP to specific endpoints
        + Needed to configure
            ++ Record Name
            ++ Record Type
            ++ Alias
            ++ Value/Route Traffic to
            ++ TTL
            ++ Routing Policy
            ++ IP-Based
            ++ Health Check ID
            ++ Record ID
    - Geoproximity Routing
        + Used to give finer-grained control of how you configure routing based on the distance between your users and your resources. Done by setting a bias.  The bias metric allows you to route traffic to specific resources

4. Know how Health Checks work
    - Health Checks monitor availability and performance of endpoints by using a network of health checks located in regions around the world
    - You can use a Domain name or an IP address and port combination to define HTTP(S) and TCP health checks.  These checks provide CloudWatch metrics to give you visibility and enable you to set alarms and notifications
    - Three types of Health Checks
        + Monitor an Endpoint:  Health check will monitor the health of an endpoint defined by IP address or domain name and a predefined interval
        + Monitor Other Health Checks (Calculated Health Checks): Can create a health check that monitors other health checks
            ++ A calculated health check can report health under three possibilities
                +++ At least X of Y selected health checks are healthy
                +++ All health checks are healthy
                +++ One or more health checks are healthy
        + Monitor CloudWatch Alarms: Health checks that can use CloudWatch metrics to determine whether an endpoint is healthy or unhealthy

5. Remember how CloudFront works
    - CloudFront is a context delivery network (CDN) service that provides security, low latencies, and high transfer speeds for your chosen dataset.  CloudFront is a global service and can be used for both distributing content from a point of origin and uploading objects when used in connection with S3 Transfer Accleration.
    - Edge Locations are the global infrastructure resource used by AWS to deliver reliable and low-latency performance worldwide.
    - A regional cache is a midpoint cache between the customer facing edge locations and the place where datasets originally live and need to be distributed.  Regional caches are usually larger in size than edge locations
    - Edge locations are protected by AWS Shield standard from DDOS attacks for free.  You can use AWS WAF to define managed rules for enhanced protection in addition to using SSL/TLS certificate support
    - CloudFront operates based on distributions the source of the data being cached, such  as an S3 bucket, datacenter server, or other web servers.  A distribution requires an origin domain to be created.
    - The cache process begins by making available the CloudFront domain name or a CNAME record for your domain name using Route 53.  When a request is made, CloudFront detects the closest edge locations and performs an origin fetch request of the data, which will then be cached on the edge location and distributed to the requesting user
    - The metrics gathered when distributing data in the cache versus performing an origin fetch is called the cache hit ratio.  Idially you would want to minimize the load on the origin server.
    - You can add Origin Shield to CloudFront which adds another layer to influence the cache hit ratio.  It reduces load on the origin server, and has better network performance.
    - CloudFront provides two ways to control access to an origin implementation using S3
        + OAI: Origin Access Identity
            ++ This is a virtual user identity used to provide your CloudFront distribution with permissions to fetch objects from an S3 bucket.  OAI prevents users from accessing your source S3 bucket directly if the S3 access URL is known, as would be the case when you upgrade access to an S3 bucket to use CloudFront.  OAI is useful to make sure your S3 data stays protected and only available using your CloudFront distribution URL.  OAI does not work well with server-side encryption using AWS KMS (SSE-KMS)
        + OAC: Origin Access COntrol
            ++ Feature to secure S3 origins by allowing access to desginated distributions only.  OAC uses IAM prinicpals to authenticate with S3 origins.  It is implemented with augmented security like short-term credentials, credential rotation, and resource-based policies.  OAC supports downloading and uploading S3 objects using SSE-KMS.  It provides comprehensive HTTP methods to support and access S3 in all AWS regions
6. Know the purpose of AWS GLobal Accelerator and when to use it
    - AWS Global Accelerator operates in a similar way to CloudFront, and it works in both directions because it is intended for your application.  Global Accelerator uses the entire AWS high-speed network to bring your applicaiton traffic requests and response items closer to customers and improve latency, agility, security, and availability.
    - Directs user request for applications service based on geographic location, application health, and routing policies that you configure.  The service also provisions static anycast IP addresses to your application so that client software will not require updates as changes take place.
    - Global Accelerator will provision two anycast IP addresses to operate as the front interface for your applications using the AWS edge network.  An anycast IP address and it allows for multiple physical destination servers to be identified by a single IP
    - Anycast IP addresses simplify allowing listing in firewalls because your only have a few anycast IP addresses to list, instead of potentially needing to list each instance or web server.
    - It can improve application performance by up to 60% and provide fast failover for multi-AZ and multiregion implementations. It also removes DNS cache dependencies so that rerouting if needed happens as fast and predictably as possible.