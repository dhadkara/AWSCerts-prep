
## Elastic Beanstalk 

AWS Elastic Beanstalk is a higher level service which allows you to quickly deploy out with minimum management effort a web or worker based environments using EC2, Docker, Elastic Load Balancing, Auto Scaling, RDS, CloudWatch etc.

### Deployment Methods

![Deployment Methods](images/eb-deployment.png)

### Customizing Elastic Beanstalk Env

- You can customize eb env using Elastic Beanstalk configuration files e.g. to install packages, create linux user/groups, run shell commands etc.)
- filename with ext of .config written in json/yaml format and must be present in <root>/.ebextensions folder.