# AWS Application integration

## Self-check

### 1. What is a message queue?

 - `Message queue` is a `form of asynchronous service-to-service communication` used in serverless and microservices architectures. It's a type of data structure that `stores messages` and allows `applications to process them asynchronously`.

 - `Message queues` provide a solution to the problem of how to `handle asynchronous tasks in distributed systems`. They allow applications to `communicate and coordinate their processes`, while `not being directly connected or dependent on each other` to be operational.

 - `How they work`:

    - An application, called the `"producer"`, sends a message and adds it to the end of the queue.
    - This `message is stored in the queue` until it is processed or deleted.
    - A different application, called the `"consumer"`, reads and processes the messages from the queue when it is ready or has the capacity to do so.
    - Once a `message is read` and processed by the consumer, it is typically `removed from the queue`.

### 2. When will you use SQS and when will you use SNS?

- `Amazon SQS` is a queue service for `handling messages between services`. It's designed for distributed computing environments, allowing components of a system to communicate asynchronously. It's typically used when there is a requirement for a specific order of operations, or when a task is computationally expensive and you want to spread the workload over time or over multiple workers.

- `Use cases for SQS`:

    - `Decoupling components` of a microservice architecture.

    - `Distributing a sequence` of tasks to be `processed in parallel`.

    - `Buffering requests`.

 - `Amazon SNS`, on the other hand, `is a publish-subscribe (pub-sub) service`. In a pub-sub model, messages are pushed to all subscribers, or to those that belong to a topic of interest. SNS is typically used when you want to send the same message to multiple recipients.

 - `Use cases for SNS`:

    - `Fanout messaging`, where an identical message needs to be sent to multiple endpoints.

    - `Sending notifications` to end users via email, SMS, or push notifications.

    - `Integrating with monitoring` systems for system-wide broadcast notifications.


- `SNS and SQS can be used together`.
    - `Example` - you can fan out messages to large numbers of subscribers in parallel via SNS, which then places these messages into individual SQS queues for processing. This allows each component to process the messages at its own pace.

### 3. Is it possible to scale an Auto Scaling Group using metrics such as SQS queue depth, or numbers of SNS messages?

 - `Yes`, you can scale an `Auto Scaling Group (ASG)` using metrics such as SQS `queue depth` or the `number of SNS messages`. You can use `Amazon CloudWatch to create alarms based on these metrics` and configure your ASG to scale in response to these alarms. When the condition in an alarm is met (for example, if the number of messages in an SQS queue exceeds a certain threshold), the alarm can trigger a scaling policy to adjust the size of the ASG.

- `SQS and SNS metrics` are available for you to monitor and create alarms on. For example, for `SQS`, you can monitor the `'ApproximateNumberOfMessagesVisible' metric` which represents the `number of messages` available for retrieval from the queue. For `SNS`, you can monitor `'NumberOfMessagesPublished'`, `'PublishSize'`, and `'NumberOfNotificationsFailed'` among others.

### 4. What is SQS pricing?

- `Amazon Simple Queue Service (SQS)` has the following pricing details:

    - `Standard Queues and FIFO Queues`:

        - The first `1 million` Amazon SQS requests `per month are free`. After that, you're charged `$0.40 per 1 million Amazon SQS requests` ($0.00000040 per request).

    - `Data Transfer OUT from Amazon SQS (per GB)`:

        - `Up to 1 GB/month` is free.

        - `The next 9.999 TB/month` is charged at $0.09/GB.

        - `The next 40 TB/month` is charged at $0.085/GB.

        - `The next 100 TB/month` is charged at $0.07/GB.

        - `Anything over 150 TB/month` is charged at $0.05/GB.

    - `Additional charges`:

        - `Content of a message` (sent or received): Free

        - `Message metadata`: Free

        - `Message attributes`: $0.06/GB

- `Note` that `AWS data transfer rates` apply for `all data transferred out over the Internet` from Amazon SQS, `except` for `data transferred to Amazon EC2 instances` or to `Amazon S3 buckets` in `the same AWS Region`.

### 5. You want to collect notifications from all your AWS regions using SNS and forward them to external system. How can you design such solution?

- `General steps`:

    - `Create a topic in SNS`: This is the channel through which your messages will be sent. When a message is published to the topic, Amazon SNS will fan out the message to all the subscribers.

    - `Create a subscription to the topic`: Subscriptions define the endpoints (like an email address, an Amazon SQS queue, or a Lambda function) to which the topic's messages will be sent. In your case, you would create a subscription that points to your external system.

### 6. What is FIFO queue?

    A FIFO (First-In-First-Out) queue is a type of queue that maintains the order of how elements are added to the queue and how they are removed. In a FIFO queue, the first element added (or the oldest element) is the first one to be removed. This is similar to real-world scenarios like waiting in line at a checkout counter – the first person in line is the first person to be served and leave the line.

- In Amazon context `Simple Queue Service (SQS)`, a `FIFO queue` is a type of queue that `precisely preserves the order of messages`. Messages sent by the sender are delivered in the same order to the receiver. This makes FIFO queues useful in scenarios where the order of operations and events is critical, such as in e-commerce applications for placing and fulfilling orders, or in financial systems where a series of transactions must be executed in the correct sequence.

- `FIFO queues` also support `message groups that allow multiple ordered message groups` within a single FIFO queue. For example, you could group orders by order ID while preserving the submission order for each group. This allows for processing of messages from different groups concurrently, increasing the throughput of the queue while still maintaining the order of messages within each group.

- One `key difference` between the standard `SQS queues` and `FIFO queues` is that while `standard queues` provide maximum throughput, best-effort ordering, and at-least-once delivery, `FIFO queues` provide the `exact order of messages and exactly-once processing`. This means that a message sent once will be delivered once and remain available until a consumer processes and deletes it, and duplicates aren't introduced into the queue.


### Documentation
- [What is Amazon Simple Queue Service](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
- [Amazon SQS FAQs](https://aws.amazon.com/sqs/faqs/)
- [Introducing Amazon Simple Queue Service (SQS) FIFO Queues – Messaging on AWS](https://www.youtube.com/watch?v=XrX7rb6M3jw&ab_channel=AmazonWebServices )
- [Amazon SQS dead-letter queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html )
- [S3 notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html)
- [Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
- [Amazon SNS FAQs](https://aws.amazon.com/sns/faqs/)
- [Event-Driven Pub-Sub with SNS and SQS](https://www.youtube.com/watch?v=c_WNBmEc6EE&ab_channel=AmazonWebServices)
- [Common Amazon SNS scenarios](https://docs.aws.amazon.com/sns/latest/dg/sns-common-scenarios.html)
- [Amazon SNS security](https://docs.aws.amazon.com/sns/latest/dg/sns-security.html)
- [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)
