## Serverless Computing

### Lambda

- AWS lambda lets you run your code without provisioning/managing servers. Only upload a code and it will run based on event triggers
- Languages supported by AWS Lambda - Node, Go, Java, Python, C# , Ruby, and PowerShell
- Event sources
  - Synchronous - Function response to events 
    - API Gateway 
    - CloudWatch logs
    - Dynamodb/Kinesis Streams
    - Cognitio
    - SQS
  - Asynchronous - Function doesn't wait for response. Set invocation-type as "Event"
    Error Handling - Can retry upto 2 times and if failed then send message to DLQ - SNS or SQS. Also Max age of event message in uprocessed queue is 6hrs.
    - SNS
    - S3
    - EC2 lifecyle events
- Limitations
  - Concurrent Execution - 1000 (default) Across all the functions in a region
    Note: If crosses concurrent execution and burst capacity then will get 429 error "Too many invocations"
  - Funtion Timeout - 3sec(default) 1sec min - 900sec max
  - Memory Allocation - 128MB min - 3008MB max in 64MB increment
  - Temp Memory - /tmp folder 512MB
- Versioning
  - Can create lambda version by publishing new version - that create a new ARN 
  - Can link version to alias so that downstream applications doesn't need to change on new version
  
  #### Layers

  - Zip archive that contains libraries, custom runtime, or other dependencies.
  - Keep the package small 
  - Can use upto 5 layers


### API Gateway
