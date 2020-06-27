## Monitoring and Reporting - 22%

### CloudWatch and CloudTrail

- Custom Metrics
    - https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/put-metric-data.html
- CloudTrail logs are encrypted by default

### ELB Monitoring

- Access Logs for Your Classic Load Balancer
    - https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/access-log-collection.html
- Request tracing for ALB
    - https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-request-tracing.html

### EBS Monitoring

- Prewarming is needed for EBS volume created from Snapshot. RAID0 increases the performance by joining more volumes
- gp1 can give 3000IOPS and go up to 16,000 IOPS by increasing size of volume but beyond it use io1 Provisioned IOPS can go upto 64,000 IOPS
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-io-characteristics.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-volume-status.html

### Elasticache Monitoring

- https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/CacheMetrics.WhichShouldIMonitor.html

### AWS Config

- https://docs.aws.amazon.com/config/latest/developerguide/iamrole-permissions.html - TODO
- https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config-rules.html
- https://docs.aws.amazon.com/config/latest/developerguide/viewing-the-aggregate-dashboard.html
- https://aws.amazon.com/config/pricing/
- https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules_getting-started.html - TODO
- https://aws.amazon.com/blogs/security/how-to-use-aws-config-to-monitor-for-and-respond-to-amazon-s3-buckets-allowing-public-access/

### AWS Trusted Advisor

- https://aws.amazon.com/blogs/aws/trusted-advisor-console-basic/

### AWS Resource Group


### Health Dashboards
- Service Health Dashboard (Overall AWS services)
- Personal Health Dashboard (Your affected services)

## High Availability - 8%

## Deployment and Provisioning - 14%

## Storage and Data Management - 12%

### S3
- S3 MFA Delete
    - https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMFADelete.html
- Access Logs
    - https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html
- Custom Access Log Information
 
 *You can include custom information to be stored in the access log record for a request by adding a custom query-string parameter to the URL for the request. Amazon S3 ignores query-string parameters that begin with "x-", but includes those parameters in the access log record for the request, as part of the Request-URI field of the log record. For example, a GET request for "s3.amazonaws.com/awsexamplebucket1/photos/2019/08/puppy.jpg?x-user=johndoe" works the same as the same request for "s3.amazonaws.com/awsexamplebucket1/photos/2019/08/puppy.jpg", except that the "x-user=johndoe" string is included in the Request-URI field for the associated log record. This functionality is available in the REST interface only.*
 
- S3 Glacier
    - https://docs.aws.amazon.com/amazonglacier/latest/dev/access-control-resource-based.html
    - https://docs.aws.amazon.com/amazonglacier/latest/dev/vault-lock-how-to-api.html

### Athena

- https://docs.aws.amazon.com/athena/latest/ug/partitions.html
- https://docs.aws.amazon.com/athena/latest/ug/columnar-storage.html

## Security and Compliance - 18%

### AWS Inspector

## Networking - 14%

### VPC

- [vpc](../vpc.md#section)
- https://aws.amazon.com/about-aws/whats-new/2019/03/announcing-multi-account-support-for-direct-connect-gateway/


## Automation and Optimization -12%

### Elastic Beanstalk

- - [elastic beanstalk](../eb.md#section)