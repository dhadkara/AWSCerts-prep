## SQS (Simple Queue Service)

Highly available distributed queue system that provides fault tolerant, loosely coupled, flexibility of distributed components of applications to send & receive without requiring each component to be concurrently available

- SQS is pull based
- Messages can be upto __256 kb__
- Messages can be kept in queue between 1min to 14days (__Default is 4days__)
- __Visibility Time Out__ 
  - is the amount of time message is invisible in queue after reader pick up the message and if message is not processed before the time out then it will be visible again in the queue
  - Visibility Time Out max is 12hrs
- Message will be processed at least once guarantee
- __Long Polling__ is basically SQS will not respond untill there is a message in a queue thus save the cost

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