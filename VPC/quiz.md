## Questions

### 1. What is the AWS resource proposed for providing access from the Internet to your instances inside the VPC?
1) NAT Gateway
2) `Internet Gateway` +
3) Egress Only Internet Gateway
4) VPC Gateway

### 2. You would like to provide access to the Internet for the EC2 instance, which launched in custom VPC with set up Internet Gateway.You see, that instance still has no access to the Internet. What is the possible reason? (Pick 2 correct answers)
1) `Route tables are missing entries` +
2) The security group doesn’t allow network in
3) `The NACL doesn’t allow traffic out` +
4) The NACL doesn’t allow traffic in

### 3. Imagine you need to connect through SSH protocol to the EC2 instance, which was launched in the private subnet. What is the possible solution to achieve this?
1) Create security group(SG) for the instance and configure inbound rule for SSH protocol
2) Set up a bastion instance in the private subnet and connect to the instance through it
3) Connect to this instance through the terminal on your local computer using SSH
4) `Set up a bastion instance in the public subnet, create SG with configured inbound rule for SSH protocol and attach it to the bastion. Create SG for the instance in private subnet and point as inbound rule the bastion instance SG` +

### 4. You would like to provide Internet access to your instances in private subnet with IPv4, while making sure this solution requires the least amount of administration and scales seamlessly. What should you use?
1) NAT Instance
2) `NAT Gateway` +
3) Egress Only Internet Gateway
4) Internet Gateway

### 5. Instance A and instance B are running in two different subnets A and B of the same VPC. Instance A is not able to ping instance B. What are two possible reasons for this? (Pick 2 correct answers)
1) `The routing table of subnet A has no target route to subnet B` +
2) The policy linked to the IAM role on instance A is not configured correctly
3) The NACL on subnet B does not allow outbound ICMP traffic
4) `The security group attached to instance B does not allow inbound ICMP traffic` +

### 6. From what services it’s possible to block incoming/outgoing IPs?
1) `Security Groups` +
2) Route 53
3) ELB
4) `NACL` + 
4) VPC Subnet

### 7. You have an EC2 Security Group with several running EC2 instances. You change the Security Group rules to allow inbound traffic on a new port and protocol, and launch several new instances in the same Security Group. The new rules apply:
1) `Immediately to all instances in the security group` +
2) Immediately to the new instances only
3) Immediately to the new instances, but old instances must be stopped and restarted before the new rules apply
4) To all instances, but it may take several minutes for old instances to see the changes

### 8. What is the difference between a security group in VPC and a network ACL in VPC (chose 3 correct answers)?
1) Security group restricts access to a Subnet while ACL restricts traffic to EC2
2) `Security group restricts access to EC2 while ACL restricts traffic to a subnet` +
3) Security group can work outside the VPC also while ACL only works within a VPC
4) `Network ACL performs stateless filtering and Security group provides stateful filtering` +
5) `Security group can only set Allow rule, while ACL can set Deny rule also` +

### 9. A benefits enrollment company is hosting a 3-tier web application running in a VPC on AWS, which includes a NAT gateway in the public Web tier. There is enough provisioned capacity for the expected workload tor the new fiscal year benefit enrollment period plus some extra overhead Enrollment proceeds nicely for two days and then the web tier becomes unresponsive, upon investigation using CloudWatch and other monitoring tools it is discovered that there is an extremely large and unanticipated amount of inbound traffic coming from a set of 15 specific IP addresses over port 80 from a country where the benefits company has no customers. The web tier instances are so overloaded that benefit enrollment administrators cannot even SSH into them. Which activity would be useful in defending against this attack?
1) Create a custom route table associated with the web tier and block the attacking IP addresses from the IGW (internet Gateway)
2) Change the EIP (Elastic IP Address) of the NAT gateway in the web tier subnet and update the Main Route Table with the new EIP
3) `Create an inbound NACL (Network Access control list) associated with the web tier subnet with deny rules to block the attacking IP addresses` +

### 10. You have a web server and an app server running. You often reboot your app server for maintenance activities. Every time you reboot your app server, you need to update the connect string for the web server since the IP address of the app server changes. How do you fix this issue?
1) Allocate and IPv6 IP address to the app server
2) Allocate an Elastic Network Interface to the app server
3) `Allocate an elastic IP address to the app server` +
4) Run a script to change the connection

### 11. What happens to the EIP address when you stop and start an instance?
1) The EIP is released to the pool and you need to re-attach it
2) The EIP is released temporarily during the stop and start
3) `The EIP remains associated with the instance` + 
4) The EIP is available for any other customer

### 12. How many Internet gateways can be attached to your custom VPC?
1) `1` +
2) 2
3) 3
4) 1 per availability zone

### 13. In a default VPC, all EC2 instances are assigned with 2 IP addresses at launch. What are they?
1) `Public IP address` +
2) `Private IP address` +
3) Elastic IP address
4) IPv6 address

### 14. A subnet can span multiple AZ
1) true
2) `false` +
