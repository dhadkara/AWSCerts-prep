## Kinesis

Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information.

- Data is processed in “shards” – with each shard able to ingest 1000 records per second.
- There is a default limit of 500 shards, but you can request an increase to unlimited shards.
- A record consists of a partition key, sequence number, and data blob (up to 1 MB).
- Transient data store – default retention of 24 hours, but can be configured for up to 7 days.

__Kinesis Data Streams__

- One shard provides a capacity of 1MB/sec data input and 2MB/sec data output.
- One shard can support up to 1000 PUT records per second.
- Kinesis Data Streams supports resharding, which lets you adjust the number of shards in your stream to adapt to changes in the rate of data flow through the stream.
  - Two types of resharding operations
    - In a __shard split__, you divide a single shard into two shards.
    - In a __shard merge__, you combine two shards into a single shard.
- __Server-side encryption__ is a feature in Amazon Kinesis Data Streams that automatically encrypts data before it's at rest by using an AWS KMS customer master key (CMK) you specify.

__Kinesis Data Firehose__

- There are no Shards, it’s completely automated (scalability is elastic).Fully managed service.
- Load data into RedShift, S3, Elasticsearch, or Splunk.
- Near real-time (60 seconds latency).
- Supports many data formats (pay for conversion). You pay for the amount of data going through Firehose.

__Kinesis Data Analytics__

- Use SQL query to query data within Kinesis (Streams and Firehose).
- Use for real-time analytics on Kinesis streams using SQL.
- Fully managed service. Provides auto scaling. Continuous: real-time.
- Can create streams out of the real-time queries.

__Kinesis Client Library__

- Kinesis Client Library is a Java library that helps read records from a Kinesis Stream with distributed applications sharing the read workload.
- The KCL is different from the Kinesis Data Streams API that is available in the AWS SDKs.
    - The Kinesis Data Streams API helps you manage many aspects of Kinesis Data Streams (including creating streams, resharding, and putting and getting records).
    - The KCL provides a layer of abstraction specifically for processing data in a consumer role.