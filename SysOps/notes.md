## Monitoring and Reporting

### CloudWatch and CloudTrail
- Custom Metrics
    - https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/put-metric-data.html
- Access Logs for Your Classic Load Balancer
    - https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/access-log-collection.html

### EBS Monitoring

- Prewarming is needed for EBS volume created from Snapshot. RAID0 increases the performance by joining more volumes
- gp1 can give 3000IOPS and go up to 16,000 IOPS by increasing size of volume but beyond it use io1 Provisioned IOPS can go upto 64,000 IOPS
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-io-characteristics.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-volume-status.html

### Elasticache Monitoring

- https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/CacheMetrics.WhichShouldIMonitor.html

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

### Inspector

