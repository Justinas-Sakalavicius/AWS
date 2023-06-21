## Self check:

1. Between block, file, object, which AWS services are related to each type?
2. What's the difference between EBS and EC2 Instance store?
3. If you need to have a folder, that will be used across a number of instance, what service will you use?
4. How can you replicate an EBS volume?
5. You have a static pages you want to expose to the Internet, what will you use for that case?
6. What are buckets in S3?
7. What does S3 replication do? What is it for?
8. What are versions in S3? What does it mean to delete an object in S3 when versioning is enabled?
9. How is it possible to optimize cost of S3 resources?
10. How nested file hierarchies are represented in S3?
11. What does S3 store inside its objects?
12. Why S3 is better than a physically maintained file server?
13. How many ways to allow access to S3 bucket do you know?
14. Is it possible attach EBS volume to a few instances simultaneously?
15. What is the use scenario for each Amazon FSx file system type?


## Between block, file, object, which AWS service are related to each type?
Block Storage: AWS provides block storage through the Amazon Elastic Block Store (EBS) service. Block storage is typically used in scenarios where you need to store data in structured blocks within sectors and tracks, such as databases. It's usually associated with Storage Area Network (SAN) environments.
File Storage: AWS provides file storage through the Amazon Elastic File System (EFS) service. File storage is commonly used for storage environments where data is organized in a hierarchical format, in files and folders. It's typically associated with Network Attached Storage (NAS) environments.
Object Storage: AWS provides object storage through the Amazon Simple Storage Service (S3) service. Object storage is used in scenarios where you need to store data as objects (which includes the data, metadata, and a unique identifier), not in files or blocks. It's suitable for scalable, unstructured data storage and is often used for web data, backups, archives, analytics, IoT, and much more.

## What's difference between EBS and EC2 Instance store ?
Persistence: Amazon EBS volumes are persistent. They exist independently of the life of the instance. If the instance fails or is stopped, the data on EBS volumes is preserved and can be attached to another instance. On the other hand, EC2 Instance Store provides temporary block-level storage. If the instance fails or is stopped, the data on Instance Store volumes is lost. Hence, Instance Store volumes are ideal for temporary storage and for data that is replicated across a fleet of instances.
Performance: Instance Store volumes can deliver very high input/output operations per second (IOPS) and are ideal for workloads where the data is frequently accessed and where speed is important. EBS volumes can also deliver high IOPS, but the performance is dependent on the type of EBS volume used (e.g., gp2, io1, etc.).
Backups: EBS volumes can be easily backed up using EBS snapshots, which can be used to create new EBS volumes or protect data for compliance purposes. However, Instance Store volumes do not support snapshots.
Size and Scale: EBS volumes can be provisioned at a size of your choosing, up to a limit of 16 TiB (for gp2 and io1 volumes, as of my knowledge cutoff in September 2021). They can also be dynamically increased in size without needing to stop your instance. Instance Store sizes, however, are determined by the instance type.
Cost: You pay for the amount of provisioned storage on EBS, whether you use it or not. In contrast, the cost of Instance Store volumes is included in the cost of the instance itself, so there is no additional charge for the storage.
Availability: Not all instance types have Instance Store volumes. When you need to use instance storage, you must select an instance type that includes instance storage.

## If you need to have a folder, that will be used across a number of instances, what service will you use ?

If you need a shared folder that will be used across a number of EC2 instances, you can use Amazon Elastic File System (EFS). EFS is a scalable file storage service for use with Amazon EC2 and other AWS services.
With EFS, you can create a file system, mount the file system on your instances, and then read and write data from and to your file system. You can mount an EFS file system in your VPC, through the Network File System versions 4.0 and 4.1 (NFSv4) protocol.
The data stored in Amazon EFS is distributed across an unconstrained number of storage servers, which helps to provide significant scalability and reliability. EFS automatically scales to petabytes of capacity, has high availability and durability, and supports multiple EC2 instances from multiple Availability Zones accessing the file system at the same time.
In addition, EFS supports file-level locking, strong read-after-write consistency, and allows concurrent connections from multiple EC2 instances. This makes it suitable for a wide variety of use cases, such as content management, web serving, data analytics, and many others.