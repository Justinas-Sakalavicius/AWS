# FAQ
## Theory
- #### What is the difference between EC2 instance connect, session manager, SSH client, and EC2 serial console?
> // TODO
- #### Can we change the key pair or user data of the running instance?
>  // TODO
- #### What is the root storage device of the instance?
>  // TODO
- #### Why after stopping and starting the instance it’s its public IP change?
> // TODO
- #### Is it right to use the same key pairs for two instances?
> // TODO
- #### How EC2 connect command is formed? Why sometimes does it contain ec2-user and sometimes root? How user data is applied?
> // TODO
- #### How we can debug 'user-data' script?
> // TODO
## Practice
- #### When we are trying to connect EC2 instance from browser using http everything is ok, but when we are requesting with https connection is refused. What is the reason?
> // TODO
- #### When we try to assign instance the s3 readonly IAM role, we see in the list only roles related to EC2 services (no any S3 roles). How is it possible to resolve this issue?
> // TODO
- #### Is it possible to see the log?  For example, We've added user data (script) and instance doesn't work properly. We've connected to this instance through the putty and execute the steps from the user data script and instance starts to work. How we can investigate the reason why user data doesn't work?
> // TODO
- #### How to properly debug the user data script execution? Is where a way to quickly reset an instance to it's original state to ensure that user data script works as intended?
> // TODO
- #### How to correctly stop load balancer with started EC2 instances?
> // TODO
