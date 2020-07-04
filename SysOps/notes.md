## Monitoring and Reporting - 22%

### CloudWatch and CloudTrail

- Custom Metrics
    - https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/put-metric-data.html
- CloudTrail logs are encrypted by default
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-recover.html
- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html

### ELB Monitoring

- Access Logs for Your Classic Load Balancer
    - https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/access-log-collection.html
- Access Logs for Your ALB
    - https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-access-logs.html
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

- https://docs.aws.amazon.com/config/latest/developerguide/iamrole-permissions.html
- https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config-rules.html
- https://docs.aws.amazon.com/config/latest/developerguide/viewing-the-aggregate-dashboard.html
- https://docs.aws.amazon.com/config/latest/developerguide/authorize-aggregator-account-console.html
- https://aws.amazon.com/config/pricing/
- https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules_getting-started.html 
- https://aws.amazon.com/blogs/security/how-to-use-aws-config-to-monitor-for-and-respond-to-amazon-s3-buckets-allowing-public-access/

### Systems Manager (SSM)
- https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances.html
- https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html

### AWS Trusted Advisor
- https://aws.amazon.com/blogs/aws/trusted-advisor-console-basic/

### Service Catalog
- https://docs.aws.amazon.com/servicecatalog/latest/adminguide/introduction.html

### Health Dashboards
- Service Health Dashboard (Overall AWS services)
- Personal Health Dashboard (Your affected services)

### Cost and Billing
- https://docs.aws.amazon.com/cur/latest/userguide/detailed-billing-migrate.html
- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/gs_monitor_estimated_charges_with_cloudwatch.html#gs_creating_billing_alarm
- https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/ce-default-reports.html#ce-ri-reports


## High Availability - 8%

- https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIT.html
- https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html
- https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html
- https://docs.aws.amazon.com/redshift/latest/mgmt/enhanced-vpc-routing.html

### AWS Support Plans
- https://aws.amazon.com/premiumsupport/plans/

## Deployment and Provisioning - 14%

### EC2
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-instance-store.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/burstable-performance-instances-unlimited-mode.html

### Auto Scaling
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroupLifecycle.html
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/schedule_time.html
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-suspend-resume-processes.html
- https://docs.aws.amazon.com/cli/latest/reference/autoscaling/update-auto-scaling-group.html

### Load Balancers
- https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/config-conn-drain.html
- https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-delete.html
- https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-security-policy-table.html

## Storage and Data Management - 12%

### S3
- S3 MFA Delete
    - https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMFADelete.html
- Access Logs
    - https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html
- Custom Access Log Information
 
 *You can include custom information to be stored in the access log record for a request by adding a custom query-string parameter to the URL for the request. Amazon S3 ignores query-string parameters that begin with "x-", but includes those parameters in the access log record for the request, as part of the Request-URI field of the log record. For example, a GET request for "s3.amazonaws.com/awsexamplebucket1/photos/2019/08/puppy.jpg?x-user=johndoe" works the same as the same request for "s3.amazonaws.com/awsexamplebucket1/photos/2019/08/puppy.jpg", except that the "x-user=johndoe" string is included in the Request-URI field for the associated log record. This functionality is available in the REST interface only.*
 - https://docs.aws.amazon.com/AmazonS3/latest/dev/DataDurability.html
 - https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-arn-format.html
 - https://aws.amazon.com/blogs/aws/amazon-s3-block-public-access-another-layer-of-protection-for-your-accounts-and-buckets/

- S3 Glacier
    - https://docs.aws.amazon.com/amazonglacier/latest/dev/access-control-resource-based.html
    - https://docs.aws.amazon.com/amazonglacier/latest/dev/vault-lock-how-to-api.html

### Athena

- https://docs.aws.amazon.com/athena/latest/ug/partitions.html
- https://docs.aws.amazon.com/athena/latest/ug/columnar-storage.html

## Security and Compliance - 18%

### IAM
- [iam](../iam.md#section)
- https://aws.amazon.com/premiumsupport/knowledge-center/authenticate-mfa-cli/

### AWS Inspector
- https://docs.aws.amazon.com/inspector/latest/userguide/inspector_introduction.html

### AWS GuardDuty
- https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html
- https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_upload_lists.html
- GuardDuty rules can't be disabled or deleted but can be auto archived so furthur findings from rule will not be displayed on console or send to CloudWatch events.

### AWS WAF vs Shield vs Firewall Manager
- https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html

### AWS Artifact
- https://docs.aws.amazon.com/artifact/latest/ug/what-is-aws-artifact.html

## Networking - 14%

### VPC

- [vpc](../vpc.md#section)
- https://aws.amazon.com/about-aws/whats-new/2019/03/announcing-multi-account-support-for-direct-connect-gateway/
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html
- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-migrate-ipv6.html
- https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html
- https://docs.aws.amazon.com/streams/latest/dev/vpc.htmls

### Route 53
- https://aws.amazon.com/premiumsupport/knowledge-center/fail-over-s3-r53/

## Automation and Optimization -12%

### Elastic Beanstalk

- - [elastic beanstalk](../eb.md#section)