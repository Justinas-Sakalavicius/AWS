# AWS  Database Services

## Self-check
### 1. What's the difference between Relational, NoSQL and In-Memory databases?

Relational, NoSQL, and in-memory databases are all types of databases used to store and retrieve data, but they differ in their structure, storage model, scalability, and use-cases.

`Relational Databases:`

    Relational databases, such as MySQL, Oracle, and PostgreSQL, use a relational model where data is stored in tables and the relationship between data is also stored in tables. Each table has a schema that defines the structure of data in that table. These databases use SQL (Structured Query Language) for defining and manipulating the data.

- Structure: Relational databases are table-based, meaning data is organized into tables which consist of rows and columns. Each column represents an attribute and each row represents a single record.

- Scalability: They are typically scaled vertically by increasing the hardware capabilities of a single server.

- Use cases: They are often used when data integrity is crucial, such as in banking systems or for any application where data needs to be consistent and transactions need to be atomic.

`NoSQL Databases:`

    NoSQL (Not Only SQL) databases, such as MongoDB, Cassandra, and Redis, are non-relational and can handle unstructured data. They don't use tables for data storage and can be schema-less.

- Structure: NoSQL databases have various data models such as document, key-value, wide-column, or graph. They are designed to be flexible, scalable, and able to handle large volumes of data.

- Scalability: They are designed to be scaled out over many servers, making them a good fit for big data and real-time applications.

- Use cases: They are often used when large amounts of distributed data are to be handled, or when the data model is subject to frequent changes, such as for social networks, real-time analytics, and big data applications.

`In-Memory Databases:`

    In-memory databases, such as Redis and SAP HANA, store data in main memory rather than on disk, leading to much faster data access and manipulation.

 - Structure: The structure can vary, and many in-memory databases support various data models, including relational and NoSQL models.

 - Scalability: They can be scaled up by adding more memory or scaled out by distributing data across multiple servers.

 - Use cases: They are often used when high-speed data access, storage, and manipulation are needed, such as in caching, session management, gaming, real-time analytics, and high-frequency trading.

### 2. If you need to store simple data(string/integer) in cache, will you use Redis or Memcached?

    If you only need to store simple data (strings/integers) in the cache and don't need the additional features provided by Redis, then Memcached could be a simpler and sufficient solution for you.

`Redis:`

 - Redis not only supports simple key-value data but also more complex types such as lists, sets, sorted sets, and hashes.

 - Redis allows you to persist your data to the disk. This means that in the event of a system failure, you won't lose all your data. However, this feature is optional and can be turned off if the durability of data is not a concern.

 - Redis supports transactions, which means that you can group several operations to be executed as a single atomic operation.

 - Redis supports master-slave replication.

`Memcached:`

- Memcached only supports simple key-value data.

- Memcached does not support data persistence. If the system fails or restarts, all data stored in the cache will be lost.

- Memcached does not support transactions.

- Memcached doesn't natively support replication, though there are third-party solutions available.

### 3. When you want to make sure you get the latest data from DynamoDB, which type of read will you use?

 ***If the latest data is critical for your application, it would be best to use a strongly consistent read**.

`DynamoDB offers two types of read consistency:`

- E`ventually Consistent Reads (Default):` The result might not reflect the results of a recently completed write operation. The results might include some stale data. However, if you repeat your read request after a short time, the response should return the latest data.

 - `Strongly Consistent Reads:` A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read. Strongly consistent reads might have higher latency and consume twice the read capacity units as eventually consistent reads, but they ensure that you always get the latest data.

### 4. Can you make your DynamoDB highly available? If yes, how?

  `Yes`, Amazon DynamoDB is designed to be highly available and durable. 
  
  - Here's how it achieves this:

    - `Multi-AZ Replication`: DynamoDB automatically replicates data across multiple Availability Zones (AZs) in a region to ensure high availability and data durability. Each AZ is a separate geographic area, and each one is isolated from the failures of the others. If one AZ experiences an outage, your data is still accessible from the other AZs.

    - `Global Tables`: If you need higher availability and data is accessed from multiple geographic locations, you can use DynamoDB Global Tables feature. This feature allows you to have DynamoDB tables that are automatically replicated across multiple AWS regions. This not only increases availability, but it also improves local read performance for global users.

    - `Backup and Restore`: DynamoDB provides on-demand and continuous backups for your data. On-demand backups allow you to create full backups of your data for long-term retention and archival for regulatory compliance needs. Continuous backups enable point-in-time recovery (PITR), allowing you to restore your table to any second in the past 35 days, providing protection from accidental writes or deletes.

    - `DynamoDB Streams`: This feature captures table activity, and you can design applications to consume these streams and take action based on the updates. This could be useful for maintaining data consistency in complex applications.

### 5. How can you backup Database services?

- `Amazon RDS` manages backups, software patching, automatic failure detection, and recovery.

  1) Manual Backups
  2) Automated Backups
  3) Snapshot Backups
  4) Continuous Backups
  5) Replication
  6) Third-Party Tool
  
### 6. What is RDS? What engines does it support? 

  ![](images/aws-dbs.png) 
  
    Amazon RDS supports the following database engines:

  - Amazon Aurora: Amazon's proprietary database engine compatible with MySQL and PostgreSQL.

  - MySQL: One of the most popular open-source relational database systems.

  - PostgreSQL: An advanced, enterprise-class, and open-source relational database system.

  - MariaDB: A community-developed fork of MySQL, led by the original developers of MySQL.

  - Oracle Database: A popular commercial relational database system.

  - SQL Server: Microsoft's relational database management system.

  - DB2 (on Linux, UNIX, and Windows servers): IBM's database software, primarily used for running online transaction processing (OLTP) and data warehousing workloads.

### 7. What is RDS pricing? 

    There are two main pricing models for Amazon RDS:

 - `On-Demand Instances`
 - `Reserved Instances` - long term cheaper.

### 8. Can you make your RDS instance highly available? If yes, how?

  `Yes`, you can make your Amazon RDS instance highly available and fault-tolerant. 

  - Here's how:
    - `Multi-AZ Deployments`
    - `Read Replicas`
    - `Automated Backups and Database Snapshots`
    - `Proactive Monitoring and Alerts`

### 9. What is read replica in RDS and how it works? 

      A Read Replica in Amazon RDS is an asynchronous copy of the master database. When you create a Read Replica, you're creating a separate DB instance that mirrors the data of the primary DB instance. The purpose of a Read Replica is to handle read-heavy database workloads, offloading the read traffic from the primary database to one or more Read Replicas, thereby increasing the aggregate read throughput and ensuring high availability.

   - Here's how it works:
  1) `Asynchronous Replication`: The primary DB instance performs all writes and updates. These changes are then asynchronously replicated to the Read Replica(s). Because this replication is asynchronous, changes made to the primary DB instance should be eventually consistent with the Read Replica, but there might be some latency, which means the Read Replica might lag slightly behind the primary DB instance.

  2) `Offloading Reads`: By directing read traffic to the Read Replica(s), you can increase the aggregate read throughput of your applications. This is particularly useful for applications with heavy database read operations, such as complex analytic queries or reporting tasks.

  3) `Scaling and Performance`: If your application's workload is read-heavy, you can create multiple Read Replicas and distribute your read traffic among them, effectively scaling your read capacity. This can help improve the performance of the primary DB instance because it can focus on write operations.

  4) `Data Protection and Availability`: Read Replicas also provide a way to protect your data. If your primary DB instance fails, you can promote a Read Replica to become the new primary DB instance with minimal downtime.

  5) `Geographic Distribution`: Read Replicas can also be created in different geographic regions than the primary DB instance. This can reduce latency for users accessing your applications from different geographical locations, and also provide additional disaster recovery capabilities in case of a regional failure.

### 10. What RDS operational (maintenance, monitoring) practices do you know? 

      Amazon RDS is designed to simplify many of the operational tasks associated with managing databases. 

 - Several best practices and operational tasks that you should keep in mind when using RDS:
    1) `Automated Backups and Snapshots`
    2) `Multi-AZ Deployments`
    3) `Read Replicas`
    4) `Regular Monitoring`
    5) `Logs and Events`
    6) `Performance Insights`
    7) `Database Maintenance`
    8) `Security Practices`
    9) `Optimization and Performance Tuning`
    10) `Resource Scaling`

### 11. What RDS capacity planning best practices do you know? 

    Capacity planning for Amazon RDS involves accurately predicting your future needs in terms of compute, memory, storage, and I/O operations to ensure that your RDS instances can handle the load and performance requirements of your applications. 
    
  - Best practices for capacity planning with Amazon RDS:
    1) `Understand Your Workload`
    2) `Monitor Usage and Performance Metrics`
    3) `Plan for Growth`
    4) `Choose the Right DB Instance Type`
    5) `Provision Enough Storage`
    6) `Use Read Replicas for Read-Heavy Workloads`
    7) `Consider Multi-AZ Deployments for High Availability`
    8) `Review and Adjust Regularly`

### 12. What RDS testing and profiling best practices do you know? 

    Testing and profiling are important aspects of managing Amazon RDS instances to ensure they meet your application's performance and availability requirements. 
    
  - Best practices for testing and profiling with Amazon RDS:
    1) `Testing in a Non-Production Environment`
    2) `Load Testing`
    3) `Performance Benchmarking`
    4) `Use AWS Performance Insights`
    5) `SQL Query Profiling`
    6) `Test Failover`
    7) `Monitor and Review Performance Metrics`
    8) `Test Scaling Operations`

### 13. What are the advantages of RDS over manually managed databases? 

    Amazon RDS provides several advantages over manually managed databases, especially when it comes to management and operational efficiency.
    
  - Key advantages:
    1) `Managed Service`
    2) `Ease of Use`
    3) `Scalability`
    4) `High Availability and Reliability`
    5) `Security`
    6) `Automated Backups and Snapshots`
    7) `Performance Insights`
    8) `Cost-Efficient`
    9) `Integration with AWS Ecosystem`

### 14. What is the difference between multi-AZ deployment and read replicas in RDS? 

    Multi-AZ deployments and Read Replicas in Amazon RDS serve different purposes and are used in different scenarios. 

  - Comparison:
    1) `Multi-AZ Deployments:`
      - Multi-AZ deployments are primarily used for high availability and failover support. In a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica of your DB instance in a different Availability Zone. The primary DB instance is synchronously replicated across Availability Zones to a standby replica to provide data redundancy, eliminate I/O freezes, and minimize latency spikes during system backups.

      - In the event of planned database maintenance, DB instance failure, or an Availability Zone failure, Amazon RDS automatically performs a failover to the standby, ensuring that your database operations can resume quickly without manual intervention.

      - Multi-AZ deployments are a good fit for production workloads where downtime and data loss cannot be tolerated.
    2) `Read Replicas:`
      - Read Replicas, on the other hand, are primarily used to offload read traffic from your primary database instance. You can create one or more replicas of a given source DB Instance and serve high-volume application read traffic from multiple copies of your data, thereby increasing aggregate read throughput.

      - Read Replicas are not used for automatic failover and do not protect against DB instance failure or Availability Zone failure. However, in the event of a failure of the primary DB instance, you can manually promote a Read Replica to become the new primary.

      - Read Replicas can also be used for disaster recovery purposes, or to maintain a copy of your data in a separate region for geographic redundancy.

      - They can also be used for reporting or data warehousing scenarios where you may want to run heavy analytics queries against the replica, offloading that work from the primary database.

  
  - `Summary`

        Use Multi-AZ deployments for high availability and automatic failover, and use Read Replicas to increase read capacity and to offload read traffic or heavy analytics queries from the primary database. 


### 15. What security features does RDS provide? 

    Amazon RDS provides a variety of features to help secure your databases. 

  - `Network Isolation`
  - `Encryption at Rest and in Transit`
  - `IAM Authentication`
  - `Resource-Level Permissions`
  - `VPC Security Groups`
  - `DB Security Groups`
  - `Automated Backups`
  - `Amazon RDS Event Notifications`
  - `Monitoring and Logging`

### 16. What is AWS Aurora? 

    Amazon Aurora is a fully managed relational database service provided by AWS. It's compatible with MySQL and PostgreSQL.

  - Key features of Amazon Aurora:
    - `Performance` Amazon Aurora offers up to five times the performance of MySQL and three times the performance of PostgreSQL
    - `Compatibility` with MySQL and PostgreSQL.
    - `Scalability` 
    - `Durability and Availability`
    - `Security`
    - `Fully Managed` hardware provisioning, database setup, patching, and backups
    - `Serverless`  is an on-demand, auto-scaling configuration that automatically adjusts database capacity based on application needs

### 17. You need to make a snapshot in RDS at a specific time, is that possible? If yes, how?

 - `Yes`, it is possible to create a snapshot of your Amazon RDS instance at a specific time. 

   - `Manual way` - with AWS Management Console, or with AWS CLI or SDKs with command `create-db-snapshot`.

   - `Automate way` - with `Lambda functions` to take snapshot, and setup a `CloudWatch Event rule` to trigger Lambda function.