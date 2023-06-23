## Self-check

### 1. What is the difference between IAM identity and IAM principle?

    In a nutshell, an `IAM identity` is a specific `type of principal that is created and managed by AWS IAM`. A `principal`, on the other hand, is a broader term that `includes not only IAM identities` but also other `types of users` and `entities` that can interact with AWS resources.


  - `IAM Identity`: An IAM identity is an entity that you create in AWS to represent the person or service that interacts with AWS products. An IAM identity can be a user (an individual person), a group (a collection of users), or a role (which you can assume to take on permissions temporarily). Each identity can have specific permissions and policies attached to it to dictate what resources they can and can't interact with. It can be used to determine who is authenticated (signed in) for a given interaction with any AWS service.

  - `IAM Principal`: The term "principal" in IAM refers more generally to an entity that is allowed to interact with AWS resources. This could be an IAM user, an IAM role, a federated user, an AWS service, an anonymous user, or even an AWS account root user. In policy language, the principal is the entity that the policy is giving permission to. It's part of the JSON policy document which is used for granting permissions.

### 2. Which type of request to AWS is recorded by CloudTrail?

  - `AWS CloudTrail` is a service that provides `event history` of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command-line tools, and other AWS services. 

        By default, CloudTrail logs management events!

 - `The actions recorded` by AWS CloudTrail are typically referred to as `"events"`. There are two types of events that CloudTrail captures:
    - `Management Events:` These represent the management operations performed on resources in your AWS account. They are also known as "control plane" operations. These include actions like creating and deleting EC2 instances or S3 buckets, modifying security groups, and so on.

    - `Data Events:` These represent the data plane operations on the resources. Data events provide insight into the resource operations performed on or in a resource itself. These include actions like S3 object-level API activity (such as GetObject, DeleteObject, and PutObject API operations), and Lambda function execute API activity.

### 3. What's the difference between customer managed IAM policy and AWS managed IAM policy?

- `In AWS Identity and Access Management (IAM)`, policies define how identities (users, groups, and roles) can interact with `AWS resources`. There are two types of managed policies you can attach to an IAM identity: 

    - `AWS Managed Policies`
        - These are `created and managed by AWS`. AWS maintains and updates these policies when new services or actions are introduced. They are designed to provide permissions for many common use cases. For example, there's an AWS managed policy called `"ReadOnlyAccess"` that gives read-only access to all AWS services.

    - `Customer Managed Policies`
        - These are `created and managed by the user` (i.e., the AWS customer). You have full control over these policies, which means you can create, update, and delete them as you see fit. These are typically used when the AWS managed policies do not meet your specific needs and you need a higher degree of customization for your permissions.

- Here are a few additional differences:

    - The `AWS managed policies` can be attached to `multiple users, groups, and roles` in your AWS account, and even across `multiple accounts` if you allow it. However, if you need fine-grained control and want to create a custom policy document, then you'll need to create a customer managed policy.

    - The `number of customer managed policies` you can create in an AWS account is `limited`, while you can use any number of AWS managed policies.

### 4. How does inline policy differ from managed policy?

 - `Inline policies` and `managed policies` in AWS Identity Access Management (IAM) offer `different ways to attach permissions to an identity` (which can be a user, group, or role).

 - `Inline Policies`: These are policies that you can create and manage, and they are directly attached to a single user, group, or role. An inline policy is embedded directly into a single entity and does not exist independently. This means that if you delete a user, group, or role, all inline policies attached to it are also deleted. Inline policies are useful when you want to maintain a strict one-to-one relationship between a policy and the entity it's applied to.

 - `Managed Policies`: Managed policies are standalone identity-based policies that you can attach to multiple users, groups, or roles. There are two types of managed policies: AWS managed policies (created and managed by AWS) and customer managed policies (created and managed by you). Managed policies offer more flexibility and are easier to work with when you need to assign the same set of permissions to multiple entities.

 - Here are a few `additional differences`:

    - `Scope`: Managed policies can be attached to multiple identities, whereas inline policies are specific to a single identity.

    - `Maintenance`: Managed policies can be easier to work with if you need to change permissions often, as the changes are automatically applied to all identities the policy is attached to. With inline policies, you would need to change the policy for each identity individually.
    - `Deletion`: Deleting a managed policy does not delete the identities it's attached to, but deleting an identity does delete any inline policies attached to it.
    - `Use Case`: Inline policies are often used for special cases where a policy is strictly tied to a single identity and doesn't need to be reused for other identities.

### 5. What are the limits for inline IAM policy?

 - The `limits` for inline IAM policies are as follows:
    - `You can use as many inline policies as you want`, but the aggregate policy size can't exceed the character quotas.
    - The inline policy `character limits` are 2,048 characters for users, 10,240 characters `for roles`, and 5,120 characters `for groups`

 - It's also worth mentioning that the maximum limit for `attaching a managed policy` to an `IAM role` or `user` is `20`. The `maximum character size limit` for `managed policies` is `6,144 characters`. The `default limit` for managed policies is `10`, and to increase this default limit from 10 to up to 20, you would need to submit a request for a service quota increase.

### 6. What are the best practices when working with permissions?

 - `Key best practices`:

    - `Least Privilege`: Grant only the permissions required to perform a task. Don't give extra permissions that a user or service doesn't need. This minimizes the potential impact if an entity's credentials are compromised.

    - `Use Groups and Roles`: Assign permissions to groups or roles, rather than individual users, whenever possible. This helps in managing permissions across multiple users.

    - `Use Managed Policies`: Use AWS managed policies when possible for common job functions, and customer-managed policies for more specific or unique cases. This can make policies easier to manage and update.

    - `Regularly Review and Update`: Regularly review and update IAM policies, roles, and credentials to ensure they're still required and are following the principle of least privilege.

    - `Remove Unnecessary Credentials`: Remove IAM user credentials (passwords and access keys) that are not needed. For example, if a user is only intended to access AWS via SSO, they do not need IAM credentials.

    - `Use Temporary Security Credentials`: Use IAM roles and temporary security credentials for applications that run on Amazon EC2 instances, instead of long-term access keys.

    - `Rotate Credentials`: Regularly rotate security credentials (like IAM user access keys).

    - `Monitor Activity`: Use services like AWS CloudTrail, AWS Config, and AWS GuardDuty to monitor and log activity related to access and permissions.

    - `Use Multi-Factor Authentication (MFA)`: Enable MFA for all IAM users, especially those with high-level privileges.

    - `Use IAM Roles for Applications`: If you have applications running on AWS services like EC2 or Lambda, assign IAM roles to those resources to grant them the necessary permissions. This is more secure and more maintainable than using access keys.

    - `Segregate Duties`: Segregate duties among AWS users to minimize the impact of errors or compromises. For example, the person who sets up and manages IAM permissions should be different from the person who uses those permissions to deploy and manage applications.

    - `Avoid Root Account`: Avoid using your AWS root account for day-to-day tasks. The root account has unlimited permissions, so it's best to use it only for necessary tasks and to otherwise leave it inactive.

### 7. The AWS CLI credentials and configuration settings take precedence in which order?(name first 3)

 - The `AWS Command Line Interface (CLI)` uses a set of rules to determine where to get the AWS credentials (Access Key ID and Secret Access Key), the AWS region, and other configuration settings. This is also known as the `"credentials lookup order"`.

 - Here's the `order of precedence for AWS CLI` (for the first three):
    - `Command Line Options`: These are the settings directly passed in the command. These options include specifying credentials, region, output format, and other options while executing a command. They have the highest precedence.

    - `Environment Variables`: If you don't specify options at the command line, the AWS CLI looks for environment variables. This includes `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`, `and AWS_DEFAULT_REGION`.

    - `CLI Credentials File`: If there are no command line options or environment variables set, the AWS CLI looks for the credentials file. The default location for the file is `~/.aws/credentials` on Linux or macOS, and `C:\Users\USER_NAME\.aws\credentials` on Windows. This file can contain credentials for multiple profiles, and you can specify which profile to use by setting the `AWS_PROFILE environment` variable or by passing a profile name with the `--profile <profile_name>` option.

 - `After the first three`, there are additional fallback mechanisms including the CLI configuration file `(~/.aws/config)`, instance profiles for EC2 instances, ECS container credentials, and more. 

### 8. What is the allow/deny priority order when policies are configured on different levels (group, user, etc.)?

 - When evaluating `AWS Identity and Access Management` (IAM) policies, AWS uses an `"explicit deny" mechanism`. This means that regardless of where the policy is applied (user, group, or role level), if there is an explicit deny, it will always take `precedence` and `override any allows`.

 - `basic evaluation logic`:

    - `Explicit Deny`: If a policy explicitly denies access to a resource, the user or role will not have access to it, even if another policy explicitly allows access. This is true regardless of where the policy is attached, whether it's to a user, a group, or a role.

    - `Explicit Allow`: If there is no explicit deny, but there is an explicit allow, the action is allowed.

    - `Implicit Deny`: If there are no policies that explicitly allow or deny access, access is implicitly denied.

 - `Attached policies` to a user directly, and `policies attached` to groups that a user is a member of, all apply to the user. `The combined permissions` grant the effective `permissions` for that user. However, if there is an explicit deny in any of these policies, it `overrides any allows`.

 - `Note` that AWS IAM `doesn't have a specific order` in which it `evaluates policies`. All policies are evaluated and a decision is made according to the above logic.

### Documentation

* [AWS Intro to IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
* [AWS Policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html)
* [AWS IAM FAQs](https://aws.amazon.com/iam/faqs/)
