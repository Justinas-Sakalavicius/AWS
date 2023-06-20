# VPC - A virtual network dedicated to your AWS account.
### 1. What kinds of IP addresses does AWS VPC offer?

  - Private IPv4 addresses: These are not reachable over the internet and are used for communication between instances within the VPC. Each instance launched into a VPC is assigned a primary private IP address from the IPv4 address range of the subnet​​.

  - Public IPv4 addresses: These are automatically assigned to a network interface created in a subnet if that subnet has the attribute to automatically assign public IP addresses enabled. A public IP address is mapped to the primary private IP address through network address translation (NAT)​​.

  - Elastic IP addresses (IPv4): These are static, public IPv4 addresses that are associated with your AWS account rather than a specific instance, and can be dynamically remapped to another instance. Elastic IP addresses remain associated with an instance when it is stopped and restarted, and they are not released when the instance is terminated, unlike regular public IP addresses​​.

  - IPv6 addresses: If an IPv6 CIDR block is associated with your VPC and your subnet, your instance in a VPC can receive an IPv6 address. IPv6 addresses are static by default and persist when you stop and start your instance​​.

### 2. What happens to different IP address types when an EC2 instance is rebooted, stopped, started? 

  - When an EC2 instance is rebooted, stopped, or started, the behavior of the different IP address types are as follows:
    
    1) Private IPv4 addresses: The private IPv4 address remains associated with the network interface even when the instance is stopped and restarted. The private IP address is only released when the instance is terminated.

    2) Public IPv4 addresses: If an instance is associated with a public IP address from Amazon's pool of public IP addresses, the public IP address is released back into the pool and is no longer available for the instance when it is stopped and started again. The instance will receive a new public IP address upon restart. However, the public IP address remains associated with the instance when it is rebooted.

    3) Elastic IP addresses (IPv4): Elastic IP addresses remain associated with the instance when it is stopped and restarted, unlike regular public IP addresses. Therefore, if an instance is associated with an Elastic IP address, it retains the same public IP address through a stop and start cycle, as well as a reboot.

    4) IPv6 addresses: IPv6 addresses persist when you stop and start your instance. The IPv6 address remains associated with the network interface during a reboot, stop, and start cycle​.

### 3. Can you assign multiple IP addresses to an instance?

  - Yes, you can assign multiple IP addresses to an instance in AWS. These can be multiple private IPv4 addresses, multiple Elastic IP addresses (public IPv4), or multiple IPv6 addresses.

  1) When you launch an instance into a VPC, a primary private IP address from the IPv4 address range of the subnet is assigned to the default network interface of the instance. You can assign additional private IP addresses, known as secondary private IP addresses, to instances that are running in a VPC. 

  2) For public IPv4 addresses, you can associate an Elastic IP address with your instance or its network interface.

  3) IPv6, if an IPv6 CIDR block is associated with your VPC and subnet, your instance can receive multiple IPv6 addresses. You can manually assign an IPv6 address to your instance during launch, assign an IPv6 address to your instance after launch, or assign an IPv6 address to a network interface in the same subnet and attach the network interface to your instance after launch

### 4. How many elastic IPs is it possible to create per account/region?

  - The default limit for Elastic IP addresses per region is 5. However, this limit is adjustable, meaning that you can request an increase if needed. 

### 5. What's the difference between Public and Private subnet?

  - **public subnet** is a subnet that is associated with a route table that has a route to an Internet Gateway

  - **private subnet**  is a subnet that is associated with a route table that doesn’t have a route to an Internet Gateway. Therefore, resources in private subnets cannot communicate directly with the public internet. AWS resources within the same VPC CIDR can communicate via their private IP addresses. However, resources in a private subnet can use a NAT Gateway to communicate with the Internet, with the NAT Gateway being deployed in a public subnet. Any AWS resources that don’t need access to the public internet should run in a private subnet, such as your application servers or your database​.

### 6. How do VPC subnets map onto AZs?

  - subnet is always associated with a single Availability Zone (AZ).
  - If you want to deploy your services across multiple AZs for redundancy and high availability, you would need to create multiple subnets, each in a different AZ. This way, your Virtual Private Cloud (VPC) which can span multiple AZs, will have different subnets in different AZs, allowing you to distribute your resources across these AZs.

### 7. What's the difference between Default and Custom VPC?

 - **main** differences between a default VPC and a custom VPC in AWS are related to their configuration and the level of control you have over the networking environment.

 - **Overall**, a default VPC is designed for ease of use, while a custom VPC offers more flexibility and control over your network configuration. You might use a custom VPC when you have specific networking requirements not met by the default VPC, such as a larger or smaller IP address range, specific subnet structure, or more complex networking setup.

### 8. What is the difference between NAT gateways and NAT instances?

  - A Network Address Translation (NAT) gateway and a NAT instance both allow instances in a private subnet to connect to the internet or other AWS services, but they prevent the internet from initiating a connection with those instances. However, there are several differences between a NAT gateway and a NAT instance:

    1) **Availability and redundancy** - NAT gateway is highly available and redundant within a single Availability Zone (AZ). It automatically scales to handle up to 45 Gbps of bandwidth. In contrast, a NAT instance is just a regular EC2 instance that you are responsible for managing. It doesn't automatically scale and is not redundant. If you want redundancy, you need to manually implement it by launching NAT instances in multiple AZs.
    2) **Maintenance** -  With a NAT gateway, AWS handles all the operational burden. You don't need to worry about patching the operating system or software, or managing the underlying infrastructure. With a NAT instance, you are responsible for these tasks because it's just a regular EC2 instance.
    3) **Performance** - NAT gateways offer better performance and can handle a higher rate of connections compared to NAT instances.
    4) **Cost** - Both NAT gateways and NAT instances incur costs, but the pricing models are different. You pay for each NAT gateway-hour that your NAT gateway is provisioned and available. Data processing and data transfer costs also apply. NAT instance costs are based on the cost of the EC2 instance you choose to run as your NAT.
    5) **Security Groups** - NAT instance can be associated with security groups.
    6) **Bastion Servers** - You can use a NAT instance as a bastion server to allow Secure Shell (SSH) access to instances in your VPC for management tasks. A NAT gateway doesn't support this because you can't assign a public IP address to it.
    7) **Port Forwarding** - NAT instances can be used for port forwarding.
    8) **Traffic Metrics** - With NAT gateways, you can obtain Amazon CloudWatch metrics such as bytes transferred and error counts, which is not as straightforward with NAT instances.

### 9. Suppose you’ve assigned a CIDR block to a VPC. Will all the IPs in that block be available for the resources you create in the VPC?

  - **No**, not all the IP addresses in the CIDR block you assign to your VPC will be available for you to use with your resources. AWS reserves the first four IP addresses and the last one in each subnet CIDR block. These addresses are not available for you to use and cannot be assigned to an instance.

### 10. When will you use NACL and when will you use SG? Which of them is stateful and which one is stateless? 

  - Network Access Control Lists (NACLs) and Security Groups (SGs) are both types of firewalls that provide security at different levels of the network for your Amazon VPC.

    **Network Access Control Lists (NACLs)**:

     - NACLs are applied at the subnet level, so they provide an additional layer of security if an instance's security group rules are accidentally modified.
     - NACLs are stateless. This means that any changes you make to the inbound rules don't automatically apply to the outbound rules. If you want to allow both inbound and outbound traffic, you need to explicitly create rules in both directions.
     - NACLs have the ability to deny traffic. They include an ordered list of rules, and the first rule that matches the traffic is the one that's applied. This means you can create a rule to deny traffic from a certain IP address, and then a rule to allow all traffic, and the deny rule will be applied first to the traffic from that IP address.

    **Security Groups (SGs)**:

     - Security Groups are applied at the instance level, so they provide more granular control than NACLs.
     - Security Groups are stateful. This means that if you allow inbound traffic from a certain IP address, that address is automatically allowed to send outbound traffic, too. Conversely, if you send outbound traffic to a certain IP address, that address is automatically allowed to send inbound traffic to you.
     - Security Groups can only allow traffic, they cannot deny traffic. If there's no rule that allows a particular type of traffic, that traffic is automatically denied.

  - In terms of when to use each, it depends on your use case. As a best practice, you can start by setting broad restrictions with NACLs at the subnet level (like denying all traffic from certain IP addresses known to be associated with malicious activity), and then use Security Groups to set more granular permissions at the instance level.

### 11. How does VPC determine whether to deny/allow a request when both ACLs and security groups specified?


  - When both Network Access Control Lists (NACLs) and Security Groups are specified, **AWS VPC uses them in combination** to determine whether to allow or deny a request.

    Here's how it works:

    - NACLs: These are the first line of defense. If an incoming request is explicitly denied by the NACL rules, the request is dropped right there and not passed further. The NACL rules are evaluated in order of their rule number, and the first rule that matches the request is applied. If a request is allowed by the NACL, it is then passed on to the Security Group associated with the instance.

    - Security Groups: These act at the instance level. Once the request passes the NACL, it is evaluated by the Security Group rules. If the Security Group rules allow the request, it is forwarded to the instance; otherwise, it is dropped.

    It's important to note that both NACLs and Security Groups must allow the request for it to reach the instance. If either the NACLs or Security Groups deny the request, it will not reach the instance.

    Additionally, keep in mind that NACLs are stateless (each request is evaluated independently, without considering any previous requests), whereas Security Groups are stateful (responses to allowed inbound traffic are automatically allowed to flow out, and vice versa).

### 12. What does "local" target mean in terms of an AWS routing table?

  - In an AWS routing table, the "local" target represents a rule that allows communication within the same network (VPC). It's a default rule that cannot be modified or removed.

### 13. How do you connect your VPC to the Internet?

 1) **Create an Internet Gateway and attach it to your VPC** - An Internet Gateway serves two purposes: to provide a target in your VPC route tables for internet-routable traffic, and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.
 2) **Create a Route Table** - A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. By default, your VPC has a main route table that you can modify.
 3) **Add a route to the Main Route Table for your VPC** -  You can add a route that points all traffic (0.0.0.0/0) to the internet gateway.
 4) **Subnet's Network Access Control List (NACL) and Security Groups** - Ensure that your NACL and security groups allow the relevant traffic to flow in and out of your VPC.
 5) **Assign a Public IPv4 address or Elastic IP address to your instance** - To enable an instance to communicate with the internet, it must have a public IP address or an Elastic IP address that's associated with a private IPv4 address for the instance.

  -  Keep in mind that while your VPC can access the internet, individual instances within it cannot unless they're specifically set up with the correct routing and IP addressing.

### 14. What is bastion in terms of networking?

  - cloud services, a bastion host is often used as a secure, controlled entry point to a virtual private cloud (VPC) environment from an external network, such as the Internet. This is useful for example when you need SSH or RDP access to EC2 instances which are not assigned public IP addresses for security reasons. Instead of allowing inbound traffic to all the instances in the VPC, you allow inbound SSH or RDP traffic to the bastion host, and from there, you can access the other instances in the VPC.

### 15. How can you monitor the network traffic in VPC?

  - You can monitor the network traffic in your AWS VPC (Virtual Private Cloud) using several tools and services provided by AWS:

    1) VPC Flow Logs
    2) Amazon CloudWatch
    3) AWS CloudTrail
    4) Amazon GuardDuty
    5) AWS Network Firewall
    6) Traffic Mirroring

### 16. Can you peer VPC with a VPC belonging to another AWS account?

  - **Yes** you can peer a Virtual Private Cloud (VPC) with a VPC that belongs to another AWS account. This is known as inter-account VPC peering. It allows network traffic to flow directly between the peered VPCs in a private and secure manner. This can be useful in scenarios such as when two different departments of an organization have separate AWS accounts but need to share resources.

### 17. Do you pay for VPC when using EC2 instances?

  - **No**, you do not pay for the VPC itself when using EC2 instances. The use of Amazon VPC and its features do not incur additional costs. **However**, data transfer and other services within VPC, such as NAT gateway or VPC endpoints, do come with their own costs. Also, the EC2 instances that you run within the VPC are separately billed.