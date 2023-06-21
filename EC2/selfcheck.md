## Self-check:
- What is EC2?

  `EC2` (Elastic Compute Cloud): This service provides resizable compute capacity in the cloud, making it easy to deploy and manage applications.
- What are the types of EC2 instances?

  1) `General Purpose Instances`: These instances provide a balance of compute, memory, and networking resources and can be used for a wide range of applications.

  2) `Compute Optimized Instances`: These instances are optimized for compute-intensive workloads and applications. They have a high ratio of compute resources to memory resources.

  3) `Memory Optimized Instances`: These are designed for tasks that require a lot of memory. They're ideal for applications that process large datasets in memory. 

  4) `Storage Optimized Instances`: These instances are designed for workloads that require high, sequential read and write access to very large data sets on local storage.

  5) `Accelerated Computing Instances`: These instances use hardware accelerators, or co-processors, to perform functions such as floating-point number calculations, graphics processing, or data pattern matching, more efficiently than software on a general-purpose CPU.

  6) `Arm-based Instances`: These instances are powered by AWS Graviton2 and Graviton Processors that are custom built by AWS utilizing 64-bit Arm Neoverse cores. 

- What provisioning/billing options are available with EC2?

  1) `On-Demand Instances` - Pay, by the second, for the instances that you launch.

  2) `Reserved Instances` - Reduce your Amazon EC2 costs by making a commitment to a consistent instance configuration, including instance type and Region, for a term of 1 or 3 years.

  3) `Spot Instances` - Request unused EC2 instances, which can reduce your Amazon EC2 costs significantly.

  4) `Dedicated Hosts` - Pay for a physical host that is fully dedicated to running your instances, and bring your existing per-socket, per-core, or per-VM software licenses to reduce costs.

  5) `Dedicated instances` - Pay, by the hour, for instances that run on single-tenant hardware.

  6) Capacity Reservations – Reserve capacity for your EC2 instances in a specific Availability Zone for any duration.
 
- How to reduce costs when purchasing EC2 instances?

  Use savings plans for reducing your Amazon EC2 costs by making a commitment to a consistent amount of usage, in USD per hour, for a term of 1 or 3 years.

- What are Regions and Availability zones, and how can it help to build high availability solutions?

   AWS has the concept of a `Regions`, which are a separate geographic areas of the world where we cluster data centers. Each group of physical data centers is called an  `Availability Zone`.
   Each AWS Region consists of multiple, isolated, and physically separate AZs.
   `Each AZ` has independent power, cooling, and physical security and is connected via redundant, ultra-low-latency networks. AWS customers focused on high availability can design their applications to run in multiple AZs to achieve even greater fault-tolerance. 

- What keys are created for each EC2 instance? What for?

  When you create an Amazon EC2 instance, you are prompted to create and download a key pair. This key pair consists of a `public key` that AWS stores, and a `private key` file (.pem) that you store.

  The key pair is `used to` securely SSH (Secure Shell) into your instance. Without the private key, you cannot SSH into your instance.

- What happens to EC2 instances when they are stopped and started vs re-started?

  1) `Stop`: When an EC2 instance is stopped, the instance performs a normal shutdown and then transitions to a stopped state. All of its Amazon EBS volumes remain attached, and you can start the instance again at any time. You're not charged for additional instance hours while the instance is in a stopped state.

  2) `Start`: When you start a stopped instance, it enters the pending state, and then the running state. The instance retains its instance ID, but it may have a different public IP address, private IP address, and MAC address. If the instance is in a VPC and is associated with an Elastic IP address, then the IP address remains associated with the instance when it's stopped and restarted.

        When you `reboot (or restart)` an EC2 instance, it remains on the same host computer and keeps its public IP address, private IP address, and any data on its instance store volumes. Rebooting an instance doesn't affect the Amazon EBS volumes attached to the instance or the data on those volumes.

- What is the difference between IAM roles and EC2 (VPC) security groups?

  `IAM roles` are about permissions and access control within and between AWS services.

  `EC2 security groups` are about controlling network access to instances.

- What is AMI? How it differs from Snapshot(or from Launch Template)?

  `Amazon Machine Image` (AMI) 

  `Difference from snapshot:`
  
  - AMI is a template for the root volume for the instance (i.e., the operating system, the applications, and the application server), while a snapshot is a copy of a volume.

  - You can launch multiple instances from a single AMI while you can use a snapshot to create a new volume (which can be then attached to an instance).

  - An AMI can be made public and shared with other AWS accounts, while snapshots can be shared with others but cannot be made public.

  `Difference from a Launch Template:`

  - An AMI is a software configuration for an instance, while a Launch Template contains the information needed to launch an instance, such as instance type, key pair, security groups, and which AMI to use.

  - You can't launch an instance from an AMI without specifying additional parameters like instance type, key pair, and security groups. A Launch Template stores all this information, so you can launch instances with a single command or a few clicks in the AWS Management Console.

- What is EBS? What types of volumes are offered by EC2?

  `EBS Snapshot`: is a backup of a single EBS volume.
  1) General Purpose SSD - default EBS volume type for Amazon EC2 instances. 

  2) Provisioned IOPS SSD - deliver high performance for I/O intensive workloads, such as databases.

  3) Throughput Optimized HDD - magnetic storage volumes that are ideal for frequently accessed, throughput-intensive workloads such as big data, data warehouses, and log processing.

  4) Cold HDD - magnetic storage volumes that provide the lowest cost per gigabyte of all EBS volume types.

  5) Magnetic - previous generation volumes that are suited for workloads where data is accessed infrequently, and applications where the lowest storage cost is important.

- Is it possible to decrease the size of an existing EBS volume?

  Cannot decrease the size of an Amazon EBS volume directly. However, there is a workaround to achieve a similar result, which involves creating a new, smaller volume and copying the data from the larger volume to the smaller one. 

- Is it possible to reuse a EBS volume for multiple instances?

  No, an Amazon Elastic Block Store (EBS) volume can only be attached to one EC2 instance at a time. However, you can detach an EBS volume from one instance and then attach it to another instance.

- How can you monitor EC2 instances?

  `Yes`

- What is horizontal scalability and Amazon EC2 auto scaling?

  `Horizontal scalability` - This refers to the ability of a system to increase its capacity by adding more hardware or instances. 

  `EC2 auto scaling` - This is a feature provided by Amazon Web Services (AWS) that allows you to automatically scale your Amazon EC2 capacity up or down according to conditions you define. With EC2 Auto Scaling, you can ensure that you have the right number of Amazon EC2 instances available to handle the load for your application.

- What is Load Balancer? What types of Amazon Load Balancers do you know? What is the key difference between them?

  A `load balancer` serves as the single point of contact for clients. The load balancer distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones.

  `Types of Load Balancers available:`

  1) An `Application Load Balancer` (ALB) functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action. You can configure listener rules to route requests to different target groups based on the content of the application traffic. Routing is performed independently for each target group, even when a target is registered with multiple target groups. You can configure the routing algorithm used at the target group level. The default routing algorithm is round robin; alternatively, you can specify the least outstanding requests routing algorithm.

  2) A `Network Load Balancer` (NLB) functions at the fourth layer of the Open Systems Interconnection (OSI) model. It can handle millions of requests per second. After the load balancer receives a connection request, it selects a target from the target group for the default rule. It attempts to open a TCP connection to the selected target on the port specified in the listener configuration.  
  For TCP traffic, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, destination port, and TCP sequence number. The TCP connections from a client have different source ports and sequence numbers, and can be routed to different targets. Each individual TCP connection is routed to a single target for the life of the connection.  
  For UDP traffic, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port. A UDP flow has the same source and destination, so it is consistently routed to a single target throughout its lifetime. Different UDP flows have different source IP addresses and ports, so they can be routed to different targets.

  3) A `Classic Load Balancer` is a previous generation of loadbalancers. It’s recommended to consider mentioned above types of loadbalancers instead. CLB operates on Layer 4/7 of the Open Systems Interconnection (OSI) model. The only one type of LB which is compatible with EC2-Classic

  4) `Gateway Load Balancers` enable you to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. It combines a transparent network gateway (that is, a single entry and exit point for all traffic) and distributes traffic while scaling your virtual appliances with the demand. A Gateway Load Balancer operates at the third layer of the Open Systems Interconnection (OSI) model, the network layer. It listens for all IP packets across all ports and forwards traffic to the target group that's specified in the listener rule. It maintains stickiness of flows to a specific target appliance using 5-tuple (for TCP/UDP flows) or 3-tuple (for non-TCP/UDP flows).
  Gateway Load Balancers use Gateway Load Balancer endpoints to securely exchange traffic across VPC boundaries. Traffic to and from a Gateway Load Balancer endpoint is configured using route tables. Traffic flows from the service consumer VPC over the Gateway Load Balancer endpoint to the Gateway Load Balancer in the service provider VPC, and then returns to the service consumer VPC. You must create the Gateway Load Balancer endpoint and the application servers in different subnets. This enables you to configure the Gateway Load Balancer endpoint as the next hop in the route table for the application subnet. 

  ## Key differences: 
  - Performance and flexibility : Network Load Balancers offer high performance and the ability to handle millions of requests per second. Application Load Balancers offer flexibility in managing HTTP and HTTPS traffic and provide features like content-based routing and support for container-based applications.
  - Level of traffic management: Application Load Balancers work at the application layer (layer 7), allowing them to route traffic based on the content of the request, while Network Load Balancers work at the transport layer (layer 4) and route traffic based on the IP address and port.
  - Use case
  - Features

- What is the request routing algorithm for Application and Network Load Balancers?

  - `(ALB)` The default routing algorithm is round robin

  - `(NLB)` 
    - For UDP traffic, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port. 

    - For TCP traffic, same as UDP plus TCP sequence number.

- What is a Listener and Listener rules? What is rule priority and rule condition?

  - `A listener` - is a process that checks for connection requests, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to the targets in one or more target groups.

  - `Listener Rules` - These are used to route requests to different target groups based on the content of the application traffic. Each rule consists of a priority, one or more actions, and one or more conditions. When the conditions for a rule are met, the traffic is forwarded to the corresponding target group.

  - `Rule Priority` - Each rule for a listener has a priority. The priority helps to determine the order in which the rules are evaluated. Rules are processed in priority order, from the lowest value to the highest value. The first rule that a request matches is the rule that's used to route the request.

  - `Rule Condition` - A rule condition defines how the load balancer chooses the targets when forwarding requests. For an Application Load Balancer, you can include host conditions and path conditions.

- What is a Target Group? Can you use Lambda behind the Target Group?

  - `Target group` is used to route requests to one or more registered targets, such as EC2 instances, containers, or Lambda functions. 

  - `Yes` you can use Lambda as a target for an (APL). To trigger a Lambda function, you need to grant Elastic Load Balancing permission to run the function.

- How is it possible to install/configure software on a EC2 instance?

  1) Using the Yum Package Manager

  2) Using Repositories

  3) Compiling from Source

  4) Updating Software

- How is it possible to get such metadata as current region/AZ from within a running EC2 instance?

  You can retrieve metadata such as the current region/Availability Zone (AZ) from within a running EC2 instance by accessing the instance metadata service. You can access metadata, by using a tool such as cURL in a script running on the instance.

- What are the key events in EC2 instance lifecycle?

  1) `Launch:` An instance is launched using Amazon Machine Images (AMIs), which serve as templates that contain the software configuration required to boot up an EC2 instance. It includes the operating system and any additional software needed for the instance to run properly.

  2) `Boot:` Upon launching, the EC2 instance boots the operating system and gets ready to start any services or applications.

  3) `Operate:` During this stage, the instance is running and available for use. You can connect to it, install software, and use it as per your requirements.

  4) `Stop / Start:` If you don't need to use an instance, you can stop it, which performs a normal shutdown and transitions the instance to a stopped state. When you're ready to use it again, you can start the instance, and it will transition back to the running state. Stopped instances do not incur charges, but the associated EBS volumes do.

  5) `Terminate:` When you no longer need an instance, you can terminate it. Once terminated, the instance cannot be restarted. Any data on local instance storage is lost, but data on EBS volumes can be preserved.

  6) `Reboot:` You can reboot an instance, which is equivalent to an operating system reboot. The instance remains on the same host computer and maintains its public DNS name, private IP address, and any data on its instance store volumes.

- How is it possible to grant a EC2 instance permissions to access certain AWS resources like S3?

  - To grant an EC2 instance permissions to access certain AWS resources like S3, you would typically use an IAM role. 
  
  - You can create an IAM role with the necessary permissions and then associate this role with your EC2 instance. 
