# AWS Certification Notes

* Great websites for AWS exam notes 
    - https://jayendrapatil.com/
    - https://digitalcloud.training/certification-training/aws-developer-associate/
* Course I used - acloudguru and whizlab

AWS Cert Exam Notes and Tips

# AWS Developer Associate Curriculam 

- [IAM](iam.md#section)
- [S3](s3.md#section)
- [EC2](ec2.md#section)
- [VPC](vpc.md#section)
- [Route53](route53.md#section)
- [Database](database.md#section)
- [Security](security.md#section)
- [Serverless](serverless.md#section)
- [ElasticBeanstalk](eb.md#section)
- [ApplicationServices](application-services.md#section)
- [CICD](cicd.md#section)
- [Monitoring](monitoring.md#section)
- [Kinesis](kinesis.md#section)

# AWS SysOps Associate Curriculam 

- https://jayendrapatil.com/aws-certified-sysops-administrator-associate-soa-c01-exam-learning-path/#AWS_Certified_SysOps_Administrator_Associate_SOA-C01_Exam_Contents

- [Notes](SysOps/notes.md#section)

## Generic

### SSH into EC2 terminal

- Create and Download KeyPair from AWS to e.g. ~/Downloads folder

```
chmod 400 MyKeyPair.pem
ssh ec2-user@<publicIpOfEc2> -i MyKeyPair.pem
```
- Elevate previlege to root
```
sudo su
```