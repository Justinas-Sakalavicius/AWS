# AWS Storage Services

## Self check:

### 1. Between block, file, object, which AWS services are related to each type?

 - `Block Storage`: AWS provides block storage through the Amazon Elastic Block Store (EBS) service. Block storage is typically used in scenarios where you need to store data in structured blocks within sectors and tracks, such as databases. It's usually associated with Storage Area Network (SAN) environments.
 - `File Storage`: AWS provides file storage through the Amazon Elastic File System (EFS) service. File storage is commonly used for storage environments where data is organized in a hierarchical format, in files and folders. It's typically associated with Network Attached Storage (NAS) environments.
 - `Object Storage`: AWS provides object storage through the Amazon Simple Storage Service (S3) service. Object storage is used in scenarios where you need to store data as objects (which includes the data, metadata, and a unique identifier), not in files or blocks. It's suitable for scalable, unstructured data storage and is often used for web data, backups, archives, analytics, IoT, and much more.

### 2. What's the difference between EBS and EC2 Instance store?

 - `Persistence`: Amazon EBS volumes are persistent. They exist independently of the life of the instance. If the instance fails or is stopped, the data on EBS volumes is preserved and can be attached to another instance. On the other hand, EC2 Instance Store provides temporary block-level storage. If the instance fails or is stopped, the data on Instance Store volumes is lost. Hence, Instance Store volumes are ideal for temporary storage and for data that is replicated across a fleet of instances.
 - `Performance`: Instance Store volumes can deliver very high input/output operations per second (IOPS) and are ideal for workloads where the data is frequently accessed and where speed is important. EBS volumes can also deliver high IOPS, but the performance is dependent on the type of EBS volume used (e.g., gp2, io1, etc.).
 - `Backups`: EBS volumes can be easily backed up using EBS snapshots, which can be used to create new EBS volumes or protect data for compliance purposes. However, Instance Store volumes do not support snapshots.
 - `Size and Scale`: EBS volumes can be provisioned at a size of your choosing, up to a limit of 16 TiB (for gp2 and io1 volumes, as of my knowledge cutoff in September 2021). They can also be dynamically increased in size without needing to stop your instance. Instance Store sizes, however, are determined by the instance type.
 - `Cost`: You pay for the amount of provisioned storage on EBS, whether you use it or not. In contrast, the cost of Instance Store volumes is included in the cost of the instance itself, so there is no additional charge for the storage.
Availability: Not all instance types have Instance Store volumes. When you need to use instance storage, you must select an instance type that includes instance storage.

### 3. If you need to have a folder, that will be used across a number of instance, what service will you use?

- `Amazon Elastic File System (EFS) provides` a `simple`, `scalable`, `fully managed elastic NFS file system` for use with `AWS Cloud services` and `on-premises resources`. It is built to scale on demand to petabytes without disrupting applications, growing and shrinking automatically as you add and remove files. Multiple EC2 instances (or even on-premises servers) can mount an EFS file system and have read and write access to the same set of files.

- One of the `key advantages of EFS` is that it `allows sharing of a common data source between multiple instances`. It's useful for workloads and patterns such as content management, web serving, data sharing, and many others.

### 4. How can you replicate an EBS volume?

 - To replicate an `Amazon Elastic Block Store (EBS)` volume across `Availability Zones` or even across `different AWS regions`, you can leverage `EBS snapshots`.

 - Also, the `snapshots are point-in-time copies`, so they `might not include data` that has not been written to the source EBS volume at `the time the snapshot is taken`. To `ensure` the consistency of the data, `it's recommended` to stop the instance `before taking the snapshot`, or at least ensure that the data is in a consistent state.

 - `Automating the snapshot` process can be done with `Amazon Data Lifecycle Manager (DLM)`, which can automatically manage the creation, retention, and deletion of snapshots.

### 5. You have a static pages you want to expose to the Internet, what will you use for that case?

 - If you have `static web pages` that you want to `expose to the internet`, you can use `Amazon Simple Storage Service (S3)` to `host the website`. Amazon S3 is a `highly scalable`, `reliable`, and `low-latency data storage infrastructure` at very `low costs`.

- `Steps to host a static website using Amazon S3`:

    - `Create a new S3 bucket`: Create a new bucket in the AWS Management Console. The bucket name should match the domain name you want to use for your website.

    - `Enable static website hosting for your bucket`: Go to the Properties tab of your S3 bucket, and enable "Static website hosting". As your "Index Document", you can specify something like "index.html".

    - `Upload your static web files`: Upload your static website files into your new S3 bucket. This can include HTML files, CSS, JavaScript, and image files. You can do this using the S3 Management Console, AWS CLI, or an SDK.

    - `Set the bucket policy`: You need to change the bucket permissions to allow public access to your website. This can be done by modifying the bucket policy to allow public read access to your S3 bucket.

    - `Access your website`: You can access your website using the Endpoint URL provided by S3 in the "Static website hosting" card in the bucket properties.

### 6. What are buckets in S3?

 - `Amazon Simple Storage Service (S3)`, a bucket is the basic container for your data. 


   - `Global Namespace`: Each S3 bucket you create has a globally unique name across all AWS accounts. This means that two different AWS accounts cannot have a bucket with the same name.

   - `Storage`: A bucket can store any number of objects (files), and each object can be up to 5 terabytes in size.

   - `Configuration`: Buckets have configuration properties such as their region, versioning status, access policies, and transfer acceleration status.

    - `Access Control`: You can use bucket policies and Access Control Lists (ACLs) to manage access to your S3 buckets and the objects within them.

    - `Events`: You can set up event notifications on your bucket to alert you or trigger workflows when objects are created or deleted in your bucket.

    - `Website Hosting`: Buckets can be configured to host static websites, serving your static content (HTML, CSS, JavaScript, and image files) to browsers.

### 7. What does S3 replication do? What is it for?

 - `Amazon S3 Replication` is a feature that automatically replicates (copies) objects across different S3 buckets. These buckets can be in different AWS `regions or within the same region`. There are `several types` of S3 Replication, including Cross-Region Replication (CRR) and Same-Region Replication (SRR).

    - `S3 Replication is primarily used for these purposes`:

        - `Compliance requirements`: Some organizations have data sovereignty and compliance requirements that dictate that data must be stored redundantly in multiple geographically distinct regions.

        - `Minimize latency`: Replicating data across AWS regions can help reduce latency by providing users faster access to the same data from a closer source.

        - `Operational reasons`: For example, you might want to maintain copies of your data for different purposes such as analytics, backup and restore, or for having different levels of data access.

        - `Data redundancy and backup`: To increase the durability and availability of your data, you might want to maintain a backup copy in another region or bucket.

        - `Disaster recovery`: In the event of a catastrophic failure in one AWS region, you might need to quickly switch to another region. Having a copy of your data in another region can make the recovery process faster and smoother.

   -  When you `enable replication` on a bucket, all `new objects` uploaded to the source bucket are `automatically replicated` to the destination bucket. `Existing objects` can also be replicated by creating a new `replication rule` with the existing object replication option.

### 8. What are versions in S3? What does it mean to delete an object in S3 when versioning is enabled?

 - In `Amazon S3`, `versioning is a feature` you can enable on your `S3 buckets` that keeps `multiple versions of an object in the same bucket`. This means that once you enable versioning on a bucket, `Amazon S3 preserves existing objects anytime` you perform a PUT, POST, COPY, or DELETE operation on them.

 - When you `overwrite or delete an object`, instead of `removing the existing object`, S3 `keeps all versions of an object` (including all writes and deletes) in the bucket. `Each version of an object is given a unique version ID`.

### 9. How is it possible to optimize cost of S3 resources?

 - `Several strategies` you can employ to `optimize the cost` of using `Amazon S3`:

    - `Use S3 Storage Classes`: Amazon S3 offers several storage classes that are designed for different use cases and have different pricing. For example, S3 Standard is designed for general-purpose storage of frequently accessed data, while S3 Intelligent-Tiering is designed to optimize costs by automatically moving data to the most cost-effective tier based on how frequently you access each object. S3 Glacier and S3 Glacier Deep Archive are designed for long-term archive storage and are very inexpensive, but retrieval times are longer and there are costs associated with retrieving data.

    - `Lifecycle Management`: S3 Lifecycle policies can automatically transition your data to more cost-effective storage classes or archive them after a certain time period. You can also set up rules to automatically delete data that is no longer needed.

    - `Delete Unneeded Data`: Ensure that you're not storing data that is no longer needed. Use S3 Analytics to identify infrequently accessed data that might be a candidate for moving to a cheaper storage class or deletion.

    - `Optimize Data Transfer`: Data transfer, especially when done out to the internet or across regions, can be a significant cost. Use data transfer optimization strategies, such as caching, content delivery networks (like Amazon CloudFront), and compression to reduce these costs.

    - `S3 Request Pricing`: The costs of PUT, COPY, POST, LIST, GET, and other requests can add up, particularly on buckets with a lot of traffic. Optimize your application to reduce unnecessary API requests.

    - `Enable S3 Transfer Acceleration`: If you regularly transfer large amounts of data across great geographical distances, S3 Transfer Acceleration can help speed up the process, reducing the time your data spends in transit and potentially saving you money in terms of reduced operational costs or improved user productivity.

    - `Consolidate and Compress Data`: If possible, consolidate many small files into larger ones to reduce the total number of PUT and LIST requests, and compress your data before storing it in S3 to reduce storage volume.

    - `Versioning`: If you're using versioning, remember that all versions of an object (including all writes and deletes) are kept in the bucket. This can lead to higher storage costs, so regularly clean up old versions if they're no longer needed.

### 10. How nested file hierarchies are represented in S3?

 - `Amazon S3` is a `flat storage structure` that `does not support actual nested folders or directories` like a traditional file system. `However`, you can create a logical hierarchy or simulate a folder structure using object key name prefixes and slashes (/).

 - In S3, the `name of the object` (also known as the key) is a unique identifier within each bucket. Each object in a bucket has exactly one key, and the combination of a bucket, key, and version ID uniquely identify each object.

- Example, you might have an `object` with the key `"images/nature/photo.jpg"`. Even though S3 does not actually have `nested directories`, the `slashes (/)` in the key name give the appearance of a `hierarchical structure`. So in this case, it appears as though the "photo.jpg" `object` is in the "nature" `subfolder` of the "images" `folder`.

- `This "folder" structure` is purely for `organizational purposes` and `does not affect the functionality of the bucket`. For example, you cannot set permissions on a "folder". Permissions are managed at the individual object level, or at the bucket level through bucket policies.

- When you use the `Amazon S3 console`, and when you use other programs that interact with `Amazon S3`, these `slashes (/)` are often represented as folders to make it easier for users to organize and find their objects.

### 11. What does S3 store inside its objects?

- `Amazon S3` stores data in what it calls `"objects"`. 

- `Object` in S3 consists of the following components:

   - `Key`: This is the name that you assign to an object. It is a unique identifier within each bucket. The combination of a bucket, key, and version ID (if versioning is enabled) uniquely identify each object.

   - `Value`: This is the actual data content of the object, which can be any kind of data (for example, a text file, a photo, a video, etc.). An object's value can be up to 5 terabytes in size.

   - `Version ID`: This is the identifier for an object's version, which is assigned if versioning is enabled for the bucket. Each version of an object in your bucket has a unique version ID.

   - `Metadata`: This is a set of name-value pairs with which you can store additional information about the object. Some metadata is set automatically by Amazon S3 (system metadata), such as the date last modified and the object's size. Other metadata can be specified by the user at the time the object is stored (user-defined metadata).

   - `Subresources`: Amazon S3 uses the term "subresource" to refer to object-specific additional information. For instance, an object can have access control information as a subresource. Other subresources include the object's lifecycle configuration and replication configuration.

   - `Access Control Information`: You can control who has access to an object and what actions they can perform on it through the object's access control lists (ACLs) and bucket policies.

 - When you store an object in `Amazon S3`, Amazon S3 assigns a `unique identifier` to the `object in the bucket`. Even if you `delete an object` and then s`tore another object` with the `same key`, Amazon S3 treats it as a `different object` that just happens to have the same key. If `versioning is enabled` for the bucket, `Amazon S3` assigns a `unique version ID` to the `object`.

### 12. Why S3 is better than a physically maintained file server?

 - `Amazon S3` offers several `benefits` compared to traditional, physically maintained file servers. 
 
 - `Advantages`:
    - `Scalability`: S3 can store any amount of data with virtually no limits, and can scale up and down as needed, automatically. In contrast, physical file servers have a finite amount of storage and require manual effort to increase capacity.

    - `Durability and Availability`: S3 is designed for 99.999999999% (11 nines) of durability and 99.99% availability of objects over a given year. It achieves this through redundant storage across multiple facilities within a region. On the other hand, a physical file server is subject to hardware failures and doesn't natively offer the same level of redundancy.

    - `Cost-Effectiveness`: With S3, you only pay for what you use, with no upfront costs. You can also save money by using different storage classes for different needs. A physical file server, however, requires an upfront investment in hardware and ongoing costs for maintenance, power, cooling, and IT personnel.

    - `Security`: S3 offers robust security features, including encryption at rest and in transit, bucket policies, access control lists, and integration with AWS Identity and Access Management (IAM). A physical file server requires manual security configurations and may not offer the same level of control.

    - `Global Accessibility`: S3 data can be accessed from anywhere in the world via the internet, which is not typically the case with a physical file server.

    - `Data Backup and Recovery`: S3 provides features like versioning, cross-region replication, and lifecycle management which simplify the process of backing up data and recovering it in the case of accidental deletion or a disaster. Such features are not typically available with a physical file server without additional configuration and services.

    - `Integration`: S3 easily integrates with a wide range of other AWS services, like Amazon CloudFront for content delivery, AWS Lambda for serverless computing, and Amazon Athena for querying data directly in S3.

### 13. How many ways to allow access to S3 bucket do you know?

 - Ways to manage access to `Amazon S3 buckets`:

    - `IAM Policies`: IAM policies are JSON documents that grant permissions to AWS services and resources. They define who (the principal) is allowed to do what (the action) on what resources, and under what conditions. IAM policies can be attached to IAM users, groups, or roles.

    - `Bucket Policies`: Similar to IAM policies, bucket policies are JSON documents that specify who can access a bucket and what actions they can perform. Bucket policies are attached at the bucket level.

    - `Access Control Lists (ACLs)`: ACLs provide a finer level of access control for buckets and objects. They allow you to grant specific permissions to specific AWS accounts (not IAM users) or to make an object public.

    - `Presigned URLs`: You can generate a presigned URL for a bucket or an object. This URL includes a token that grants temporary access to the bucket or object. You can specify the duration of the access.

    - `Query String Authentication`: Similar to presigned URLs, query string authentication allows you to provide time-limited access to your S3 resources by appending certain parameters in the URL.

    - `Cross-origin Resource Sharing (CORS)`: CORS is a method of allowing a client web application in one domain to access resources in another domain. It is useful if you are hosting a web-based client for your S3 bucket.

    - `Access Points`: S3 Access Points are unique hostnames attached to buckets that simplify managing data access at scale for applications using shared datasets. Each access point has distinct permissions and network controls.

    - `Public Access Settings`: You can set your bucket to public access, which means anyone can access it. However, it's important to note that allowing public access to your S3 bucket can expose your data to potential security risks, so it's not typically recommended for most use cases.

    - `VPC Endpoints`: If your bucket is intended for use by resources in a specific VPC, you can set up a VPC endpoint for S3. This allows traffic to your S3 bucket to remain within the AWS network, offering better security and sometimes performance.

- `Note`: the `"least privilege" principle` is a `key best practice in AWS` - always provide the minimal set of permissions necessary for a user or application to function. For example, it's generally better to allow access through IAM policies rather than making a bucket or object public.

### 14. Is it possible attach EBS volume to a few instances simultaneously?

 - `No`, you can't attach an Amazon Elastic Block Store (EBS) volume to multiple instances at the same time. An `EBS volume` can only be `attached` to a `single instance` at any given point in time.

 - `However`, AWS does offer a service called `Amazon Elastic File System (EFS)` that `can be mounted to multiple EC2 instances` at the same time. EFS provides a simple, scalable, and fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources.

 - If you have a `use case` where you need to `share data between instances`, `EFS` could be a suitable solution. It allows many instances to `read` and `write` to the `same set of data simultaneously`, and offers a higher degree of `concurrent access` and `higher throughput` than `EBS`.

### 15. What is the use scenario for each Amazon FSx file system type?

- `Amazon FSx` provides fully managed file storage that is accessible over several industry-standard protocols. 

- `Supports two types of file systems`: `Amazon FSx for Windows File Server` and `Amazon FSx for Lustre`.
    - `Amazon FSx for Windows File Server`: It provides fully managed, highly reliable, and scalable file storage that is accessible over the industry-standard Server Message Block (SMB) protocol. It's a good choice if you have applications that require Windows shared file storage. Common use cases include home directories, software and content repositories, and data analytics workloads.

        - `Example Scenario`: You might use FSx for Windows File Server if you're running a Microsoft-based application stack on AWS that requires shared file storage, such as a CRM or ERP system. It's also useful if you're migrating existing applications from an on-premises environment that rely on Windows-based shared file storage.

    - `Amazon FSx for Lustre`: It provides a high-performance file system optimized for fast processing of workloads such as machine learning, high performance computing (HPC), video processing, financial modeling, and electronic design automation (EDA). FSx for Lustre is designed to provide fast I/O performance (millions of IOPS) and can handle large data sets. It can be linked to an Amazon S3 bucket for long-term data storage.

        - `Example Scenario`: You might use FSx for Lustre if you're running compute-intensive workloads that require fast processing of large amounts of data. This could include tasks like genomic sequencing, seismic analysis for oil and gas exploration, or financial risk modeling.