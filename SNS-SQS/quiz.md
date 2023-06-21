## Questions

### 1. Does Amazon SNS guarantee that messages are delivered to the subscribed endpoint?

1) Yes, as long as the subscribed endpoint is accessible
2) `There is an occasional possibility that message is not delivered to subscribed endpoint because of transient network conditions` +

### 2. Which of the following statements about SQS is incorrect?

1) Amazon SQS can trigger a lambda function.
2) `All messages in Amazon SQS queue are encrypted by default.` +
3) Use dead letter queues to isolate messages that can't be processed for later analysis.
4) SQS can work as FIFO queue

### 3. How many times will a subscriber receive each message?

1) Only once
2) `There can be occasional, duplicate messages at the subscriber's end` +

### 4. Who can change permissions on a topic?

1) `Any entity that allowed to do that according to permission policy to the Amazon SNS topic` +
2) Anyone who has access to an account
3) Only the owner of the topic
4) Only root user of account

### 5. Which statement is correct?

1) `SNS stores multiple copies (to disk) of the message across multiple Availability Zones before acknowledging receipt of the request to the sender.` +
2) SNS stores copy (to disk) of the message to one Availability Zone before acknowledging receipt of the request to the sender, then propagate to other Availability Zones.
3) SNS doesn’t store a copy of the message before acknowledging receipt of the request to the sender, and then stores multiple copies (to disk) of the message across multiple Availability Zones.
4) SNS doesn’t store a copy of the message before acknowledging receipt of the request to the sender, and then stores one copy (to disk) of the message in one Availability Zone.

### 6. Amazon SQS pricing is based on a number of _______ and the amount of ______ transferred in and out.

1) Calls/messages
2) `Requests/data` +
3) Downloads/permits

### 7. To prevent messages from being lost or becoming unavailable, all messages are stored __________ across multiple servers and data centers.

1) Publicly
2) Privately
3) `Redundantly` +

### 8. A _____ letter queue is a queue that other queues can target to send messages that could not be processed successfully.

1) Broken
2) Maimed
3) `Dead` +
4) Fixed

### 9. Amazon SQS was designed to enable a/an _________ number of messaging services to read and write a/an ________ number of messages.

1) Unlimited/limited
2) `Unlimited/unlimited` +
3) Limited/unlimited
4) Limited/limited
