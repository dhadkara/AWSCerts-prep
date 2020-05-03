# AWS Certification Notes

AWS Cert Exam Notes and Tips

# AWS Developer Associate Curriculam 

- [IAM](iam.md#section)
- [S3](s3.md#section)
- [EC2](ec2.md#section)
- [KMS](kms.md#section)
- [CICD](cicd.md#section)

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