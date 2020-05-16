# AWS Certification Notes

* Great website for AWS exam notes - https://jayendrapatil.com/
* Course I used - acloudguru and whizlab

AWS Cert Exam Notes and Tips

# AWS Developer Associate Curriculam 

- [IAM](iam.md#section)
- [S3](s3.md#section)
- [EC2](ec2.md#section)
- [Database](database.md#section)
- [Security](security.md#section)
- [Serverless](serverless.md#section)
- [ElasticBeanstalk](eb.md#section)
- [ApplicationServices](application-services.md#section)
- [CICD](cicd.md#section)
- [Monitoring](monitoring.md#section)

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