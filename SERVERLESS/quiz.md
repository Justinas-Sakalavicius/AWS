## Questions

### 1. How can you increase the CPU resources for your Lambda
1) `Increase the configured memory value` +
2) Increase the configured concurrency value
3) Increase the configured CPU value
4) Increase the configured timeout value

### 2. In what style must you write Lambda code?
1) `Stateless` +
2) Stateful
3) Virtual
4) MVC

### 3. How can a developer provide Lambda code?
1) By uploading a .zip file
2) `All of these answers` +
3) By editing inline
4) From an S3 bucket

### 4. How do you author a Lambda in a programming language that AWS does not support?
1) Create a Lambda function with a custom runtime and reference the function in your Lambda
2) `Create a Lambda layer with a custom runtime and reference the layer in your lambda` +
3) You cannot use Lambda in this situation
4) Create a Lambda function with a custom runtime

### 5. How is the cost associated with Lambda function calculated? (Pick 2 correct answers)
1) `Based on the number of requests to your functions` +
2) Based on the amount of code run
3) Based on the amount of used infrastructure
4) `Based on the time it takes for your code to execute` +

### 6. You need to use a Lambda to provide backend logic to your website that is hosted outside the AWS. Which service do you use to make your Lambda available to your website?
1) S3
2) NAT Gateway
3) Internet Gateway
4) `API Gateway` +
5) SNS

### 7. A company is writing a Lambda function that will run in multiple stages, such a dev, test and production. The function is dependent upon several external services, and it must call different endpoints for these services based on function’s deployment stage. What Lambda feature will enable the developer to ensure that the code references the correct endpoints when running in each stage?
1) Tagging
2) `Environment variables, where for each stage there is a copy of it with the Lambda Alias as the suffix` +
3) Aliases
4) Concurrency

### 8. You’ve created a Lambda function with the default settings. You add code to this function which makes calls to DynamoDB. You try and test the function. But the function is not completing its execution. Which of the following might be probable causes for this? (Pick 2 correct answers)
1) `The IAM Role attached to the function does not have access to DynamoDB` +
2) `The timeout of the function has been reached` +
3) You need to deploy the function first
4) You need to create a version for the function first

### 9. Your team is developing a set of Lambda functions. You need to ensure the team uses the best practices for working with AWS Lambda. Which of the following is an advantage on instantiating the AWS Client outside the AWS Lambda function handler?
1) Ability to decode errors better
2) Ability to instantiate an object for each invocation
3) `Ability to reuse Execution Context` +
4) Ability to call functions faster

### 10. Your development team is developing several Lambda functions for testing. These functions will be called by a single .NET program. The program needs to call each Lambda function in a sequential manner for testing purposes. How can you accomplish this in the easiest way to ensure that least changes need to be made to the .NET program to call the various Lambda functions?
1) Create different environment variables for the Lambda function
2) Create different versions for the Lambda function
3) `Create an ALIAS and reference is in the program` +
4) Use the SAM for deployment of the functions

### 11. A Python dependency takes 5 minutes to natively compile for Lambda and therefore deployments have been really slow. What do you suggest?
1) `Create a Lambda layer` +
2) Migrate to Node.js
3) Build the dependency on EC2
4) Store the dependency in S3
