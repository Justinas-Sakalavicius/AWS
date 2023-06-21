## Questions

### 1. What does Amazon CloudFormation provide? 

1) The ability to setup Autoscaling for Amazon EC2 instances.
2) `A templated resource creation for Amazon Web Services.` +
3) A template to map network resources for Amazon Web Services.
4) None of these.

### 2. A user is planning to use AWS CloudFormation for his automatic deployment requirements. Which of the components mentioned below are required as a part of the template?

1) `Parameters.` +
2) Outputs.
3) Template version.
4) `Resources.` +

### 3. Regarding AWS CloudFormation, what is a stack?

1) Set of AWS templates that are created and managed as a template.
2) Set of AWS resources that are created and managed as a template.
3) `Set of AWS resources that are created and managed as a single unit.` +
4) Set of AWS templates that are created and managed as a single unit.

### 4. A customer is using AWS for Dev and Test. The customer wants to setup the Dev environment with CloudFormation. Which of the below mentioned steps are not required while using CloudFormation?

1) Create a stack.
2) `Configure a service.` +
3) Create and upload the template.
4) Provide the parameters configured as part of the template.

### 5. When working with AWS CloudFormation Templates what is the maximum number of stacks that you can create?

1) 1.
2) 1-9.
3) 10-99.
4) `\>100.` +

### 6. What happens, by default, when one of the resources in a CloudFormation stack cannot be created?

1) Previously created resources are kept but the stack creation terminates.
2) Previously created resources are deleted and the stack creation terminates.
3) `Stack creation continues, and the results indicate which steps failed.` +
4) CloudFormation templates are parsed in advance, so stack creation is guaranteed to succeed.

### 7. A user has created a CloudFormation stack. The stack creates AWS services, such as EC2 instances, ELB, AutoScaling, and RDS. While creating the stack it created EC2, ELB and AutoScaling but failed to create RDS. What will CloudFormation do in this scenario?

1) CloudFormation can never throw an error after launching a few services since it verifies all the steps before launching.
2) It will warn the user about the error and ask the user to manually create RDS.
3) `Rollback all the changes and terminate all the created services.` +
4) It will wait for the user’s input about the error and correct the mistake after the input.

### 8. What is a circular dependency in AWS CloudFormation?

1) When a Template references an earlier version of itself.
2) when Nested Stacks depend on each other.
3) `When Resources form a DependOn loop.` +
4) When a Template references a region, which references the original Template. 
