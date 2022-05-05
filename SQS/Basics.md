# AWS SQS

## Introduction

Amazon Simple Queue Service (SQS) is a fully managed message queuing service.

- 4 days - Default message retention period. (Possible values 60 secs - 14 days)
- 256kb - max size of SQS messages. (Including attributes but excluding message system attributes)
- Queue name format: https://sqs.[AWS Region].amazonaws.com/[AWS Account Number]/[Queue Name] e.g https://sqs.us-east-2.amazonaws.com/123456789012/MyQueue
- The name of a FIFO queue must end with the .fifo suffix. The suffix counts towards the 80-character queue name quota.

![image](https://user-images.githubusercontent.com/33947539/166856973-af84f7f4-27e3-48e1-9405-0b7d851c2217.png)

## SQS Types

![image](https://user-images.githubusercontent.com/33947539/166858070-89a99229-98d3-47ed-94c1-9ad84d164116.png)

## How does SQS work ?

SQS provides a message-queue service. To use SQS, you need the following components:

![image](https://user-images.githubusercontent.com/33947539/166858463-03a53fc0-38b2-4e89-b6e7-985285b31e4f.png)

1. Producer(s): Producers are responsible for sending messages to a particular queue. Messages are stored in the queue when they are sent by the producer.
2. Consumer(s): Consumers are responsible for retrieving and processing the messages from a particular queue. Messages must be deleted by the consumer after processing to ensure they aren’t processed by any other consumers.

## Short and long polling

- Short polling - The default. The ReceiveMessage request queries only a subset of the servers (based on a weighted random distribution) to find messages that are available to include in the response. Amazon SQS sends the response right away, even if the query found no messages.
- Long polling - The ReceiveMessage request queries all of the servers for messages. Amazon SQS sends a response after it collects at least one available message, up to the maximum number of messages specified in the request. Amazon SQS sends an empty response only if the polling wait time expires.

When the wait time for the ReceiveMessage API action is greater than 0, long polling is in effect.
20 seconds - The maximum long polling wait time.

## Dead letter queue
Amazon SQS supports dead-letter queues, which other queues (source queues) can target for messages that can’t be processed (consumed) successfully.

The redrive policy specifies the source queue, the dead-letter queue, and the conditions under which Amazon SQS moves messages from the former to the latter if the consumer of the source queue fails to process a message a specified number of times. When the ReceiveCount for a message exceeds the maxReceiveCount for a queue, Amazon SQS moves the message to a dead-letter queue (with its original message ID). For example, if the source queue has a redrive policy with maxReceiveCount set to 5, and the consumer of the source queue receives a message 6 times without ever deleting it, Amazon SQS moves the message to the dead-letter queue.

The dead-letter queue of a FIFO queue must also be a FIFO queue. Similarly, the dead-letter queue of a standard queue must also be a standard queue.

Don’t use a dead-letter queue with standard queues when you want to be able to keep retrying the transmission of a message indefinitely. For example, don’t use a dead-letter queue if your program must wait for a dependent process to become active or available.

Don’t use a dead-letter queue with a FIFO queue if you don’t want to break the exact order of messages or operations. For example, don’t use a dead-letter queue with instructions in an Edit Decision List (EDL) for a video editing suite, where changing the order of edits changes the context of subsequent edits.

## References:

1. https://medium.com/avmconsulting-blog/deduplicating-amazon-sqs-messages-dc114d1e6545
2. http://chinomsoikwuagwu.com/2020/06/25/Amazon-Simple-Queue-Service-SQS/
3. https://stackoverflow.com/questions/28111941/sqs-delivering-a-message-only-once
