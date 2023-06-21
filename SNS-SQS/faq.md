# FAQ
## Theory
- #### SQS as an event source for Lambda. Short polling vs long polling. Reserved concurrency.
> // TODO
- #### When creating an SQS queue in the console, you can set SNS subscriptions to a specific SNS topic. Does this mean that when an item is added to this queue, the corresponding message will be automatically published to the specified SNS topic and the application code will not have to explicitly publish this message to this topic?
> // TODO
## Practice
- #### Boto3 in Python has the function receive_messages but if we have 3 messages in SQS, and we want to receive all messages using the function, boto3 receive a predictable count of messages. It receives 1 or 3 messages. Are there any practices by which we can receive a predictable number of messages?
> // TODO
