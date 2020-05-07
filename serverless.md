## Serverless Computing

### Lambda

- AWS lambda lets you run your code without provisioning/managing servers. Only upload a code and it will run based on event triggers
- Languages supported by AWS Lambda - Node, Go, Java, Python, C# , Ruby, and PowerShell
- Event sources
  - Synchronous - Function response to events 
    - API Gateway 
    - Dynamodb/Kinesis Streams
    - Cognito
    - SQS
  - Asynchronous - Function doesn't wait for response. Set invocation-type as "Event"
    Error Handling - Can retry upto __2 times__ and if failed then send message to DLQ - SNS or SQS. Also Max age of event message in uprocessed queue is __6hrs__.
    - S3
    - SNS
    - SES
    - CloudFormation
    - CloudWatch Logs
    - CloudWatch Events
    - CodeCommit
    - Sceduled Events
    - AWS config
    - EC2 lifecyle events
- Limitations
  - Concurrent Execution 
    - __1000 per sec__ (default) Across all the functions in a region
    - If crosses concurrent execution and burst capacity then will get __429 error "Too many invocations__"
    - Request concurrency guarantees that set of executions which always be available for critical function, also act as limit
  - Funtion Timeout - __3sec(default)__ 1sec min - 900sec max
  - Memory Allocation - 128MB min - 3008MB max in 64MB increment
  - Temp Memory - /tmp folder 512MB
- Versioning
  - Can create lambda version by publishing new version - that create a new ARN 
  - Can link version to alias so that downstream applications doesn't need to change on new version
  
  #### Layers
  - Zip archive that contains libraries, custom runtime, or other dependencies.
  - Keep the package small 
  - Can use upto 5 layers
  
  #### Versions
  - By default lambda has $LATEST as version and alias
  - Can publish a version and also attach alias to it. Alias has its own ARN
  - Application will not use new code with Alias on upload. If new version is published and you want to attach to same alias then needs to be done via lambda api.
  
  #### VPC aware lambda
  - Lambda can be configure for private VPC to access other resources in VPC like EC2, Databases etc.
  - To enable, provide VPC config with subnets (recommended multiple subnets) and security group with access permissions
  - Lambda use VPC info to setup ENIs with ips __(Though it is changing and you dont need to use ENI anymore)__

  #### Lambda Edge
  - Lambda@Edge allows running of code across AWS locations globally without provisioning or managing servers, responding to end users at the lowest network latency
  - Lambda function can be configured to be triggered in response to CloudFront requests
  - Lambda@Edge only supports __Node.js and Python__ for global invocation by CloudFront events at this time

### API Gateway

- AWS API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale
- API Gateway handles all of the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, authorization and access control, monitoring, and API version management.
- Supports Multiple backends
  - AWS lambda
  - Http endpoints exposed via Elastic BeanStalk, EC2 or ELB
  - Other AWS services
  - On-Prem http endpoints via public internet
- Can create two kind of APIs
  - Rest
  - Websocket
- Can deploy to Regional, Edge or private vpc
- Can create as proxy resource means all the paths are valid

