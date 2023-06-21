## Questions

### 1. What is Amazon RDS DB instance? 

1) An isolated database in the AWS Cloud.
2) `An isolated database environment in the AWS Cloud.` +
3) An isolated database table in the AWS Cloud. 

### 2. Which database engine IS NOT supported by the Amazon RDS? 

1) MySQL 
2) Oracle 
3) `SQLite` + 
4) PostgreSQL 
5) MariaDB 
6) Amazon Aurora 
7) Microsoft SQL Server 

### 3. Which DB instance storage type is the LEAST recommended by AWS and is supported only for backward compatibility? 

1) General Purpose SSD 
2) Provisioned IOPS 
3) `Magnetic` +

### 4. Which DB instance storage type is the MOST optimized for fast and consistent performance of input and output operations? 

1) General Purpose SSD 
2) `Provisioned IOPS` +
3) Magnetic

### 5. How Amazon RDS implements the Multi-AZ deployment? 

1) Amazon RDS automatically provisions and maintains an asynchronous standby replica in a different Availability Zone; 
2) Amazon RDS automatically provisions and maintains a synchronous read replica in a different Availability Zone; 
3) `Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone;` +
4) Amazon RDS automatically provisions and maintains an asynchronous read replica in a different Availability Zone. 

### 6. Which purchasing options are supported in Amazon RDS? (Select TWO) 

1) `On-Demand Instances` +
2) Dedicated Instances 
3) `Reserved Instances` +
4) Spot instances 

### 7. Which database user authentication method IS NOT supported in Amazon RDS? 

1) Password authentication 
2) `OAuth authentication` +
3) IAM database authentication 
4) Kerberos authentication 

### 8. Which statements are CORRECT about the Amazon RDS encryption limitations? (Select TWO) 

1) `You can't create an encrypted snapshot of an unencrypted DB instance.` +
2) You can disable encryption on an encrypted DB instance. 
3) You can enable encryption after the DB instance is created. 
4) `You can encrypt a copy of an unencrypted snapshot.` +
5) You can restore an unencrypted backup or snapshot to an encrypted DB instance. 

### 9. If you don't specify a preferred backup window when you create the DB instance, how Amazon RDS assigns a backup window for it? 

1) The backup window should always be specified manually, otherwise it’s not assigned. 
2) `Amazon RDS assigns a default 30-minute backup window selected at random from an 8-hour block of time for each AWS Region.` +
3) Amazon RDS assigns a default 60-minute backup window selected at random from a 12-hour block of time for each AWS Region. 
4) Amazon RDS assigns a default 60-minute backup window selected at random from an 8-hour block of time for each AWS Region. 
5) Amazon RDS assigns a default 30-minute backup window selected at random from a 6-hour block of time for each AWS Region. 

### 10. Each calendar month for 12 months starting with the date on which you create your AWS account, the Amazon RDS Free Tier allows you to use: 

1) 750 hours of Amazon RDS Single-AZ db.t2.micro Instance usage running MySQL, MariaDB, PostgreSQL, Oracle BYOL, or SQL Server (running SQL Server Express Edition). 
2) 20 GB of General Purpose (SSD) DB Storage. 
3) 20 GB of storage for your automated database backups and any user-initiated DB Snapshots. 
4) `All of above.` +
