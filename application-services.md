## SQS (Simple Queue Service)

Highly available distributed queue system that provides fault tolerant, loosely coupled, flexibility of distributed components of applications to send & receive without requiring each component to be concurrently available

- SQS is pull based
- Messages can be upto __256 kb__. Number of SQS queues could be unlimited.
- Messages can be kept in queue between 1min to 14days (__Default is 4days__)
- __Visibility Time Out__ 
  - is the amount of time message is invisible in queue after reader pick up the message and if message is not processed before the time out then it will be visible again in the queue
  - Visibility Time Out max is 12hrs
- Message will be processed at least once guarantee
- __Long Polling__ is basically SQS will not respond untill there is a message in a queue thus save the cost. To enable long polling set value of "ReceiveMessageWaitTimeSeconds" to greater than 0 and less than 20 sec.
- __You can configure an access policy that allows anonymous users to access a message queue.__
- __Amazon SQS is PCI DSS Level 1 certified and HIPAA eligible.__

Two type so queues
1. Standard 
2. FIFO

| __Standard__ | __Fifo__  | 
|-------------|------------|
| Best effort ordering | First In First Out delivery  |
| Unlimited transactions/sec | 300 transactions/sec Max|
| At least once delivery  | Exactly once processing| 

__SQS Delay Queue__ pospone delivery of new messages
  - Delivery messages are invisible to consumers for duration of delay seconnds between 0 to 900 sec max
  - Standard Queue effects the new messages only but FIFO effects all the messages
  - For applications that might be waiting on other processes to finish before consuming for SQS process

__Large SQS Messages__ 
  - between 256KB to 2GB 
  - Use S3 to store data
  - Use Amazon SQS Extended Client library for Java to manage them
  - AWS SDK Java - provide API for S3 objects operations

## SNS (Simple Notification Service)

- Amazon SNS is a web service that is used to setup, operate and send notifications from the cloud.
- SNS can also send notifications via SMS text message, email, SQS queues or to any HTTP endpoint. Or trigger Lambda functions
- Pub-sub model whereby users subscribe to topics. Instantaneous, push-based delivery.
- __SNS + SQS FAN OUT__ you can subscribe one or more Amazon SQS queues to an Amazon SNS topic from a list of topics available for the selected queue.
- SNS retry policies - Amazon SNS defines a delivery policy for each delivery protocol. The delivery policy defines how Amazon SNS retries the delivery of messages when server-side errors occur. When the delivery policy is exhausted, Amazon SNS stops retrying the delivery and discards the message—unless a dead-letter queue is attached to the subscription

| __Endpoint type__ |	__Delivery protocols__ |	__Immediate retry (no delay) phase__ |	__Pre-backoff phase	Backoff phase__ |	__Post-backoff phase__ |	__Total attempts__ |
|----|----|----|----|----|----|
| AWS-managed endpoints |	Amazon SQS	| 3 times, without delay |	2 times, 1 second apart	| 10 times, with exponential backoff, from 1 second to 20 seconds	| 100,000 times, 20 seconds apart | 100,015 times, over 23 days |

- The following HTTP POST message is an example of a Notification message to an HTTP endpoint.
```
POST / HTTP/1.1
x-amz-sns-message-type: Notification
x-amz-sns-message-id: 22b80b92-fdea-4c2c-8f9d-bdfb0c7bf324
x-amz-sns-topic-arn: arn:aws:sns:us-west-2:123456789012:MyTopic
x-amz-sns-subscription-arn: arn:aws:sns:us-west-2:123456789012:MyTopic:c9135db0-26c4-47ec-8998-413945fb5a96
Content-Length: 773
Content-Type: text/plain; charset=UTF-8
Host: myhost.example.com
Connection: Keep-Alive
User-Agent: Amazon Simple Notification Service Agent

{
  "Type" : "Notification",
  "MessageId" : "22b80b92-fdea-4c2c-8f9d-bdfb0c7bf324",
  "TopicArn" : "arn:aws:sns:us-west-2:123456789012:MyTopic",
  "Subject" : "My First Message",
  "Message" : "Hello world!",
  "Timestamp" : "2012-05-02T00:54:06.655Z",
  "SignatureVersion" : "1",
  "Signature" : "EXAMPLEw6JRN...",
  "SigningCertURL" : "https://sns.us-west-2.amazonaws.com/SimpleNotificationService-f3ecfb7224c7233fe7bb5f59f96de52f.pem",
  "UnsubscribeURL" : "https://sns.us-west-2.amazonaws.com/?Action=Unsubscribe&SubscriptionArn=arn:aws:sns:us-west-2:123456789012:MyTopic:c9135db0-26c4-47ec-8998-413945fb5a96"
}
```
- __Message Attributes__ - Message attributes are optional and separate from—but are sent together with—the __message body max size restriction 256kb__ . The receiver can use this information to decide how to handle the message without having to process the message body first.
- Each message attribute consists of the following items:
  - Name
  - Type
  - Value

- __For Amazon SNS to send notification messages to mobile endpoints__, whether it is direct or with subscriptions to a topic, you first need to register the app with AWS. To register your mobile app with AWS, enter a name to represent your app, choose the platform that will be supported, and provide your credentials for the notification service platform. After the app is registered with AWS, the next step is to create an endpoint for the app and mobile device. The endpoint is then used by Amazon SNS for sending notification messages to the app and device.


## Step Functions

- AWS Step Functions makes it easy to coordinate the components of distributed applications as a series of steps in a visual workflow.
- You can quickly build and run state machines to execute the steps of your application in a reliable and scalable fashion.
- How it works:
  1. Define the steps of your workflow in the JSON-based Amazon States Language. The visual console automatically graphs each step in the order of execution.
  2. Start an execution to visualize and verify the steps of your application are operating as intended. The console highlights the real-time status of each step and provides a detailed history of every execution.
  3. AWS Step Functions operates and scales the steps of your application and underlying compute for you to help ensure your application executes reliably under increasing demand.



