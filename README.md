# 2-14
1. Does SNS guarantee exactly-once delivery to subscribers?
No, Amazon SNS (Simple Notification Service) does not guarantee exactly-once delivery.
It offers at-least-once delivery, which means a message may be delivered more than once to subscribers. Deduplication needs to be handled by the receiving system if exactly-once processing is required.

2. What is the purpose of the Dead-letter Queue (DLQ)?
Dead-letter Queues (DLQs) capture messages that can't be processed successfully after multiple retries.
They help in debugging issues and preventing message loss.
DLQs are supported by:
SQS: Stores failed messages from other queues.
SNS: DLQs capture failed deliveries to subscribed endpoints (like Lambda).
EventBridge: DLQs can store events that fail to be delivered to targets like Lambda or Step Functions.

3. How would you enable a notification to your email when messages are added to the DLQ?
You can set up an SNS Topic to send an email when messages arrive in a DLQ:
Create a CloudWatch Alarm for the DLQ's ApproximateNumberOfMessagesVisible metric.
Set the alarm action to publish a notification to an SNS Topic.
Subscribe your email to that SNS Topic.
Confirm the email subscription when you receive the confirmation link.
