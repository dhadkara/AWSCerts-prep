## CICD 

Continuous Integration
* build
* test
* package

Continuous Deployment/Delivery

* deploy
* acceptance test
* perf test/uat test

### AWS Developer tools
- Code Commit : Git based source code repository
  - Centralized code repository (stores source code, images, binaries, library etc)
  - Manages updates from multiple users
  - Version controlled
- Code Build : Compiles code, run tests, produce packages
  - buildspec.yaml
    ```
    Add example buildspec file
    ```
- Code Deploy : Automates code deployments to any instance
  - Deployment Approaches
    - In Place - Also called rolling update. Every instance will stop and install the update.
                 Rollback is to redeploy older version
    - Blue/Green - New instance are provisioned. Blue is current and Green is new release
                 Rollback to Blue instance. So you pay for 2 envs
  - appspec.yaml - FIle defines the deployment steps
    - version
    - os
    - files - orgnized in folder like source, config, scripts etc.
    - hooks - lifecycle event hooks - have specific run order
    All of the above needs to be correct order and appspec.yaml needs to be root folder
    ```
    Add example appspec file
    ```
- Code Pipeline : Orchestrate the build, test and deployment as code changes
   - Automatically triggers pipeline on code changes
   - Integrate with AWS like code build,code deploy, cloudformation, ECS,Elastic Beanstalk & 3rd party tools    like jenkins, github 


### CloudFormation

- Yaml or Json template to provision your AWS resources
- You upload it to S3 and cloudformation runs API in template on your behalf
- Creates Stack and if fails rollback automatically

- CF template
  - Parameters - input custom values
  - Conditions - Env to deploy
  - Resources - Mandatory* - create AWS resources
  - Mappings - create custom mapping e.g. region:AMI
  - Transforms - ref code located in S3 e.g. lambda code or reusable snippet of cf code

#### Cloudformation Nested Stacks

- allow to re-use of CF code for common use cases
- Basically ref a cf template from another cf 
```
Resources:
 Type: AWS::CloudFormation::Stack
 Properties:
   TemplateUrl: https://s3.amazonaws.com/../template.yml
```