# AWS Provisioning Services

## Self-check

### 1. If you don't want to apply updates to CFN template right away, but just check the changes, what do you need?

  - If you want to check the changes to a CloudFormation template without applying the updates right away, you would use AWS `CloudFormation Change Sets`. A change set allows you to preview how proposed changes to a stack might impact your running resources. It lists the changes `AWS CloudFormation` will make to the stack, such as which resources `AWS CloudFormation` will create or delete, before deciding whether to apply those changes.

### 2. What will you do to deploy several CFN stacks at once?

  - To deploy several `AWS CloudFormation` (CFN) stacks at once, you can use `AWS CloudFormation StackSets`.

  - A StackSet is a container for `AWS CloudFormation` stacks that lets you create, update, or delete stacks across multiple accounts and regions with a single operation. You define an `AWS CloudFormation` template and use the AWS Management Console, AWS CLI, or SDKs to create a StackSet from the template. You specify the accounts (by AWS account ID) and regions where you want to create stacks, and `AWS CloudFormation` creates the stacks in all the specified accounts and regions.

  - This can be particularly useful if you need to create identical resources in different regions or accounts, such as for setting up a `multi-region`, `active application`, or `replicating infrastructure` across `different accounts`.

### 3. Can you deploy a resource on condition using CFN? If yes, how?

  - `Yes`, you can deploy resources conditionally in `AWS CloudFormation` through the use of Conditions in `your CloudFormation template`.

  - Conditions in `AWS CloudFormation` templates allow you to define circumstances under which entities (resources, outputs, etc.) should be created, based on runtime input parameters.
    - `Example of how you might define a condition`:
    
            Parameters:
            EnvType:
                Description: Environment type.
                Type: String
                AllowedValues:
                - prod
                - test
                Default: test

            Conditions: 
            CreateProdResources: !Equals [ !Ref EnvType, prod ]

            Resources: 
            MyBucket:
                Type: 'AWS::S3::Bucket'
                Condition: CreateProdResources
    
    - In this example, `EnvType` is a parameter that can be set to `prod` or `test` when the stack is launched. The `CreateProdResources` condition checks if `EnvType` equals `prod`. If it does, the resources under this condition (in this case, `MyBucket`) are created. If not, the resources are not created. So, in this case, the S3 bucket will only be created if the `EnvType` parameter is set to `prod` when the stack is launched.

    - This `feature allows` you to create templates that can be used to create stacks that have a mix of resources tailored for different environments (like test, staging, production, etc.), all from a single template.

### 4. How can you use the same template for multiple environments?

  - You can use the same `AWS CloudFormation` template for multiple environments by making use of Parameters and Conditions. Here's how you can do it:

    1) `Parameters`: Use parameters to inject environment-specific values into your CloudFormation template. Parameters allow you to pass different values when you create or update a stack. For example, you might have different instance types, VPC IDs, or database passwords for your dev, test, and production environments. You can pass these values as parameters when you launch the stack.

    2) `Conditions`: Use conditions to control the creation of resources or the setting of property values based on the parameter values. For example, you might only want to create certain resources in a production environment, or you may want to apply different settings based on the environment.

        - `Example template`:
            
                Parameters:
                Environment:
                    Type: String
                    Default: dev
                    AllowedValues: 
                    - dev
                    - test
                    - prod

                Conditions:
                IsProd: !Equals [ !Ref Environment, prod ]

                Resources:
                MyBucket:
                    Type: 'AWS::S3::Bucket'
                    DeletionPolicy: Retain
                    Properties:
                    BucketName: 
                        Fn::Sub:
                        - "${Environment}-mybucket"
                        - Environment: !Ref Environment
                    VersioningConfiguration:
                        Status: 'Enabled'
                    LoggingConfiguration:
                        DestinationBucketName: 
                        Fn::If:
                            - IsProd
                            - !Ref ProdLogsBucket
                            - !Ref NonProdLogsBucket
                        LogFilePrefix: my-app-logs/

                ProdLogsBucket:
                    Type: 'AWS::S3::Bucket'
                    Condition: IsProd

                NonProdLogsBucket:
                    Type: 'AWS::S3::Bucket'
                    Condition: !Not [ IsProd ]

        - In this example, the `Environment` parameter allows you to specify the environment. The `IsProd` condition checks whether the environment is `prod`. The `MyBucket` resource is created in all environments, and it uses the `Environment` parameter to set the bucket name. The `ProdLogsBucket` and `NonProdLogsBucket` resources are created conditionally based on the environment. The `LoggingConfiguration` property of `MyBucket` uses the `Fn::If` function to conditionally set the `DestinationBucketName` based on the environment.

        With this approach, you can `use the same template` to create different `stacks` for your `dev`, `test`, and `production` environments, and `CloudFormation` will take care of creating the appropriate resources and setting the appropriate values based on the environment.
        
### 5. Where can you view the results of template execution?

  - In AWS, you can view the results of CloudFormation template execution in the AWS Management Console, under the `AWS CloudFormation` service. After you navigate to the CloudFormation service, you'll see a list of stacks. Each stack represents a CloudFormation template that has been executed. You can select a stack to see more details about the resources that were created or updated as a result of the template execution.

    - `Steps to view the results`:

        1) `Open the AWS Management Console`.

        2) `Navigate to the CloudFormation service`.

        3) `In the navigation pane, click on "Stacks"`.

        4) `In the list of stacks`, click on the name of the stack that represents the template execution you're interested in.

        5) `On the stack detail page`, you can view information about the stack and the resources that were created or updated.

- If there were any issues during the execution of the template, those will also be displayed in the `"Events"` tab of the stack detail page. The events provide a `chronological list of stack creation or update actions`, and can be useful for `troubleshooting issues with your template`.

- You can also view the results of template execution programmatically using the AWS SDK or AWS CLI by using the `describe-stacks` command.

### Documentation: 

- [Getting started with CloudFormation (AWS docs)](https://aws.amazon.com/cloudformation/getting-started/)
- [CloudFormation Best Practices (AWS docs)](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html)
- [CloudFormation FAQs (AWS docs)](https://aws.amazon.com/cloudformation/faqs/?nc=sn&loc=5)
- [CloudFormation Tutorial by "Simplilearn" (video)](https://aws.amazon.com/cloudformation/faqs/?nc=sn&loc=5)
- [AWS Serverless Application Model (AWS docs)](https://aws.amazon.com/serverless/sam/)
- [Introducing AWS CloudFormation modules](https://aws.amazon.com/blogs/mt/introducing-aws-cloudformation-modules/)
- [Introducing a Public Registry for AWS CloudFormation](https://aws.amazon.com/blogs/aws/introducing-a-public-registry-for-aws-cloudformation/)
- [Using the AWS CloudFormation registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html)
- [Cloudformation cli installation (cfn)](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/what-is-cloudformation-cli.html)