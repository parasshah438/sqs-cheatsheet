<!DOCTYPE html>
<html>
<head>
<body>
<h1>SQS</h1>
<h4>What is SQS</h4>
<pre> 
	SQS stands for <b>Simple Queue Service</b>.
	Amazon SQS is a web service that gives you access to a message queue that can be used to store messages 
	while waiting for a computer to process them.
	Amazon SQS is a distributed queue system that enables web service applications to quickly and 
	reliably queue messages that one component in the application generates to be consumed by another component 
	where a queue is a temporary repository 
	for messages that are awaiting processing.
	SQS is a message queuing service.
	Amazon SQS is primarily designed for sending and receiving messages in a queue
</pre> 
<h4>Queue Types</h4>
<pre>
	Standard Queues (default)
	FIFO Queues (First-In-First-Out)
</pre>
<h4>Standard Queue</h4>
<pre>
<ul><li>SQS offers a standard queue as the default queue type.</li><li>It allows you to have an unlimited number of transactions per second.</li><li>It guarantees that a message is delivered at least once. 
However, sometime, more than one copy of a message might be delivered out of order.</li><li>It provides best-effort ordering which ensures that messages are generally delivered in the same order 
as they are sent but it does not provide a guarantee.</li></ul>
</pre>	
<h4>FIFO Queue</h4>
<pre>
<ul><li>The FIFO Queue complements the standard Queue.</li><li>It guarantees ordering, i.e., the order in which they are sent is also received in the same order.</li><li>The most important features of a queue are FIFO Queue and 
exactly-once processing, i.e., a message is delivered once and remains 
available until consumer processes and deletes it.</li><li>FIFO Queue does not allow duplicates to be introduced into the Queue.</li><li>It also supports message groups that allow multiple ordered message groups within a single Queue.</li><li>FIFO Queues are limited to 300 transactions per second but have all the capabilities of standard queues.</li></ul>
</pre>	
<h4>Amazon SQS Benefits</h4>
<pre>
<ul>
<li>You control who can send messages to and receive messages from an SQS queue.</li>
<li>Supports server-side encryption.</li>
<li>SQS stores messages on multiple servers for durability.</li>
<li>SQS uses redundant infrastructure to provide highly-concurrent access to messages and 
high availability for producing and consuming messages.</li>
<li>SQS can scale to process each buffered request and handle any load increases or spikes independently.</li>
<li>SQS locks your messages during processing, so that multiple producers can send and 
multiple consumers can receive messages at the same time.</li>
</ul>
</pre>
<h4>Amazon SQS work flow</h4>
<pre>
The workflow of Amazon SQS involves several key steps, allowing applications to send, receive, 
and process messages in a decoupled and scalable manner.<br>
1) Queue Creation
Set Up: A developer creates an SQS queue in the AWS Management Console or using AWS SDKs. This queue will hold the messages.<br>
2) Sending Messages
Producers: Applications (producers) send messages to the SQS queue. Each message can contain data, attributes, and metadata.
Message Attributes: Optional metadata can be included to provide additional information about the message.<br>
3) Message Storage
Queue Management: Messages are stored in the queue until they are processed or 
until their retention period expires (up to 14 days).<br>
4) Receiving Messages
Consumers: Applications (consumers) poll the queue to retrieve messages. This can be done using short 
polling (immediate response) or long polling (waits for a message).
Visibility Timeout: Once a message is retrieved, 
it becomes invisible to other consumers for a specified visibility timeout period, 
allowing the processing application to handle it without duplication.<br>
5) Processing Messages
Business Logic: The consumer processes the message according to the business logic. 
This might involve data processing, triggering other actions, or interacting with databases.<br>
6) Deleting Messages
Acknowledgment: After successfully processing the message, the consumer deletes 
it from the queue to prevent it from being processed again.
Error Handling: If processing fails, the message remains in the queue and can be retried based on the visibility timeout. 
If it fails multiple times, it can be sent to a dead-letter queue for further analysis.<br>
7) Monitoring and Scaling
CloudWatch Integration: Monitor the queue metrics using Amazon CloudWatch, 
such as message count, processing time,and error rates.
Auto-scaling: Applications can scale up or down based on the message load.<br>
8) Dead-Letter Queue Handling
Error Management: Messages that fail to process after a certain number of attempts are 
moved to a dead-letter queue for troubleshooting and analysis.<br>
9) Retries and Backoff Strategies
Retry Logic: Consumers can implement retry logic with exponential backoff strategies to handle transient failures effectively.<br>
</pre>
<h4>lifecycle of a message in SQS</h4>
<pre>
1) Queue Creation
Step: A developer creates an SQS queue (Standard or FIFO) through the AWS Management Console, CLI, or SDK.
Outcome: The queue is ready to accept messages<br>
2) Message Sending
Step: Producers send messages to the queue using the SendMessage API call.
Outcome: Messages are stored in the queue and can include attributes.<br>
3) Message Storage
Step: Messages remain in the queue until they are received or until their retention period expires (up to 14 days).
Outcome: Messages are available for consumption.<br>
4) Message Retrieval
Step: Consumers retrieve messages using the ReceiveMessage API call. 
The message becomes invisible for a defined visibility timeout.
Outcome: Messages are processed by the consumer application.<br>
5) Message Processing
Step: The consumer processes the message according to its business logic.
Outcome: Depending on the success or failure of processing, different actions will follow.<br>
6) Message Deletion
Step: After successful processing, the consumer deletes the message from the queue using the DeleteMessage API call.
Outcome: The message is permanently removed from the queue.<br>
7) Visibility Timeout Expiration
Step: If the consumer does not delete the message before the visibility timeout expires, 
the message becomes visible again.
Outcome: The message can be retrieved by the same or different consumers for processing.<br>
8) Message Failure Handling
Step: If a message fails to process after a certain number of attempts (as defined by the queue configuration), 
it can be sent to a dead-letter queue.
Outcome: Messages in the dead-letter queue can be analyzed or retried later.<br>
9) Message Retention Expiration
Step: If a message remains in the queue beyond its configured retention period (up to 14 days), 
it is automatically deleted.
Outcome: The message is permanently removed, freeing up storage.<br>
10) Monitoring and Management
Step: Use Amazon CloudWatch to monitor the queue's metrics, including the number of messages sent, 
received, and deleted, as well as any failures.
Outcome: Insights into application performance and operational health.
</pre>
</body>
</html>
