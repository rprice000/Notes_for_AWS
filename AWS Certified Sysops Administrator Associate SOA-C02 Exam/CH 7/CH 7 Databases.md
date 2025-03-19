CH 7 Databases

1. Know the engines supported by RDS
    - Amazon Relational Database Service (RDS) is a managed database service capable of running common engines
        + MySQL
        + PostgreSQL
        + MariaDB
        + Oracle
        + Amazon Aurora
        + IBM DB2
        + SQL Server

2. Be able to compare Memcached and Redis
    - Redis is a robust in-memory cache for session caching, messages queues, and leaderboards
        + Redis is highly configurable, and the configuration can be manipulated through parameter groups
        + Redis has data tiering which allows less frequently used data to be moved from memory to solid-state (SSD) storage. This reduces cost but slightly increases latency and reduces throughput for data stored in SSD
        + Redis supports clusters however it still requires a single primary for writing
        + Redis scales vertically rather than horizontally
        + Global DataStores for Redis are managed and secure read replicas, which provide for low-latency reads and disaster recovery across regions.  Each datastore is a collection of one or more clusters in a primary/secondary cluster configuration
        + MemoryDB for Redis is an in-memory durable database.  ElastiCache with Redis and MemoryDB for Redis may seem very similar, but they serve different purposes and differ significantly in durability
    - Memcached is an in-memory cache wll suited to caching relational or NoSQL database and can be used as a session store
        + AWS recommends starting with a cache.m5.large.  Then monitor the metrics memory usage, CPU utilization and cache hit rate to determine proper sizing
    - Capabilities Comparision of Redis vs Memcached
        + Redis Features
            ++ Complex data types
            ++ Encryption
            ++ Compliance Certifications
            ++ Pub/sub
            ++ Backup/Restore
            ++ Data Partitioning
            ++ Sharding
            ++ Snapshots
            ++ Replication
        + Memcached Features
            ++ Compliance Certifications
            ++ Data Partitioning
            ++ Multithreaded Architecture

3. Know what can be monitored and where to find data
    - Performance Insights is enabled by default with the free tier retention of seven days.  Performance Insights is very helpful in identifying performance bottlenecks.  Enhanced monitoring allows visibilty into OS-level metrics, whcih are not natively visible to CloudWatch.  Enhanced Monitoring could incur fees if the activity exceeds the free tier of CloudWatch.
    - Database logs can be published to CloudWatch logs for storage and real-time anaylytics.  Publishing log data will require a service-linked role

4. Have a Caching strategy Write-through vs Lazy Loading
    - Write-Through
        + Any data destined for the database is also written to the cache.  The advantage is data in the cache is always the most current
        + The model has a write penalty, meaning it takes more resources to write than to read since each write involves both the database write as well as the cache write.
        + Since the cache only has what is being written, it will have a lot of missing data, which must then be fetched on request.  Also there may be a lot of data that is written but never again requested
    - Lazy-Loading
        + Only populates the database with data that has actually been requested
        + Lazy-loading has the advantage of keeping cache sizes smaller and more relevant.  This model will have more misses and higher latency on a miss since the request must first go to the cache, then to the database, then write the data to the cache before serving the request.
        + Data in lazy-loading can become stale since writes and updates to the database are not updated in the cache until a request is made.
        + Lazy-loading is the most commonly used form of caching

5. Understand Pricing
    - RDS instances are provisioned either as on-demand or provisioned instances.  Pricing is given by the hour but is actually calculated per second, with a minimum of 10 minutes.  Several other costs are associated with RDS
        + Storage is charged per gigabyte per month based on provisioned capacity
        + Provisioned IOPS charges apply to SSD storage only whereas I/O request charges apply only to magnetic storage and are measured per 1 million per month
        + Backup storage is billed separately from provisioned RDS storage
        + Transfer charges apply when moving data to another region or to and from the Internet
    - Pricing for Aurora is different than RDS
        + Instances are billed as either provisioned on-demand instances or a provisioned Reserved instance
        + Aurora Severless is billed based on Aurora capacity units (ACUs) per hour.  An ACU is approximately 2 GB of memory with CPU and networking
        + Aurora storage is billed per gigabyte per month for actually used data storage rather than provisioned storage.  There is also a fee per million for I/O.  Aurora Global Database is an additional fee per million replicated I/Os.  Backtrack is billed per record chage stored so the cost increases the longer back you wish to be able to restore to
    - There are two billing models for ElastiCache
        + On-demand requires no commitment and you pay only for the resources used per hour Reserved nodes are billed hourly and require a one or three year commitment.  There are three reserved billing models hourly with no up-front cost, partial up-front payment with reduced hourly cost, or all up-front
        + Additional costs include a per gigabyte charge for backup
        + There is a fee for data transfer between AZs.  Global Database changes for data transfer out

6. Understand performance and cost
    - The RDS console displays several recommendations which can be found on the lower-left navigation in the console.  Trusted Advisor gives recommendations on idle RDS instance, RDS security group access risks, RDS backups, and multi-AZ RDS. Trusted Advisor will also monitor RDS service limits

7. Understand high availability and disaster recovery
    - High Availability
        + Ensures a minimal downtime and continued operation in case of hardware failure or instance failure within the same AWS region
            ++ Key Features
                +++ AWS automatically replicates data synchronously to a standby instance in a different AZ
                +++ In case of failure, AWS performs automatic failover to the standby
                +++ Used for production workloads where uptime is critical
            ++ REader Endpoints with Amazon Aurora
                +++ Aurora clusters allow read replicas across multiple AZs
                +++ Failover to a read replica is quick ensuring HA with minimal disruption
        + Primary Goal: Minimize downtime by ensuring a backup instance is always available
    - Disater Recovery
        + Ensures databases restoration and continuity in case of failure
        + Key Features
            ++ Cross-Region Replication
                +++ Replicate data asynchronously to an RDS instance in a different region
                +++ Used for disaster recovery, read scaling, and geographical redundancy
            ++ Automated and Manual Backups
                +++ Snapshots and point-in-time recovery allow restoring data even after accidental deletion or corruption
            ++ AWS Backup and Database Migration Service
                +++ Facilitates data migration and restoration across regions or AWS accounts
            ++ Primary Goal: Enable data recovery in case of a major disaster that affects an entire AWS region.
                