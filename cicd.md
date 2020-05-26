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
#### Code Commit
  - Git based source code repository
  - Centralized code repository (stores source code, images, binaries, library etc)
  - Manages updates from multiple users
  - Version controlled

#### Code Build
  - Compiles code, run tests, produce packages
  - buildspec.yaml

 ```
version: 0.2

phases:
install:

runtime-versions:

docker: 18

pre_build:

commands:

- echo Logging in to Amazon ECR...

- $(aws ecr get-login --no-include-email --region $AWS_DEFAULT_REGION)

build:

commands:

- echo Build started on `date`

- echo Building the Docker image...

- docker build -t $IMAGE_REPO_NAME:$IMAGE_TAG .

- docker tag $IMAGE_REPO_NAME:$IMAGE_TAG $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG

post_build:

commands:

- echo Build completed on `date`

- echo Pushing the Docker image...

- docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG
 ```
__Phases__:
- Install: install dependencies you may need for the build.
- Pre-build: final commands to execute before build.
- Build: actual build commands.
- Post build: finishing touches (e.g. zip file output).
- Artifacts: these get uploaded to S3 (encrypted with KMS).

You can override the default buildspec file name and location. For example, you can:
- Use a different buildspec file for different builds in the same repository, such as buildspec_debug.yml and buildspec_release.yml.
- Store a buildspec file somewhere other than the root of your source directory, such as config/buildspec.yml or in an S3 bucket. The S3 bucket must be in the same AWS Region as your build project. 

#### Code Deploy
  Automates code deployments to any instance
  EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services
                  
  - Deployment Approaches 

   1. For EC2/On-prem instances: EC2 instances are identified by CodeDeploy by using tags or an Auto Scaling Group name.
     
    - In Place - Also called rolling update. Every instance will stop and install the update.
                 Rollback is to redeploy older version
    - Blue/Green - New instance are provisioned. Blue is current and Green is new release
                 Rollback to Blue instance. So you pay for 2 envs

   2. For AWS Lambda
    
    - Used to deploy applications that consist of an updated version of a Lambda function.
    
    - Can manage the way in which traffic is shifted to the updated Lambda function versions during a deployment by choosing a canary, linear, or all-at-once configuration

   3. ECS
    
    - Used to deploy an Amazon ECS containerized application as a task set.
    
    - CodeDeploy performs a blue/green deployment by installing an updated version of the application as a new replacement task set
    
    - You can manage the way in which traffic is shifted to the updated task set during a deployment by choosing a canary, linear, or all-at-once configuration
    
    - For Amazon ECS and AWS Lambda there are three ways traffic can be shifted during a deployment:
      
      - Canary: Traffic is shifted in two increments. You can choose from predefined canary options that specify the percentage of traffic shifted to your updated Amazon ECS task set / Lambda function in the first increment and the interval, in minutes, before the remaining traffic is shifted in the second increment.
      - Linear: Traffic is shifted in equal increments with an equal number of minutes between each increment. You can choose from predefined linear options that specify the percentage of traffic shifted in each increment and the number of minutes between each increment.
      - All-at-once: All traffic is shifted from the original Amazon ECS task set /  Lambda function to the updated Amazon ECS task set / Lambda function all at once.

    __Tip: AWS Lambda and Amazon ECS deployments cannot use an in-place deployment type__

  __Deployment Group__

    Each deployment group belongs to one application and specifies:
    - A deployment configuration – a set of deployment rules as well as success / failure conditions used during a deployment.
    - In an EC2/On-Premises deployment, a deployment group is a set of individual instances targeted for a deployment. A deployment group contains individually tagged instances, Amazon EC2 instances in Amazon EC2 Auto Scaling groups, or both.
    - Notifications configuration for deployment events.
    - Amazon CloudWatch alarms to monitor a deployment.
    - Deployment rollback configuration.
   
  __Deployments__
   - Each Amazon EC2 instance must have the correct IAM instance profile attached.
   - The CodeDeploy agent must be installed and running on each instance.
  - appspec.yaml - File defines the deployment steps
    - version
    - os
    - files - orgnized in folder like source, config, scripts etc.
    - hooks - lifecycle event hooks - have specific run order
    All of the above needs to be correct order and appspec.yaml needs to be root folder

- Example of EC2/On-prem deployment appspec.yaml file
```
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html/WordPress
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: root
  AfterInstall:
    - location: scripts/change_permissions.sh
      timeout: 300
      runas: root
  ApplicationStart:
    - location: scripts/start_server.sh
    - location: scripts/create_test_db.sh
      timeout: 300
      runas: root
  ApplicationStop:
    - location: scripts/stop_server.sh
      timeout: 300
      runas: root
```
- Example of an AppSpec file written in YAML for deploying an Amazon ECS service
```
version: 0.0
Resources:
  - TargetService:
      Type: AWS::ECS::Service
      Properties:
        TaskDefinition: "arn:aws:ecs:us-east-1:111222333444:task-definition/my-task-definition-family-name:1"
        LoadBalancerInfo:
          ContainerName: "SampleApplicationName"
          ContainerPort: 80
# Optional properties
        PlatformVersion: "LATEST"
        NetworkConfiguration:
          AwsvpcConfiguration:
            Subnets: ["subnet-1234abcd","subnet-5678abcd"]
            SecurityGroups: ["sg-12345678"]
            AssignPublicIp: "ENABLED"
Hooks:
  - BeforeInstall: "LambdaFunctionToValidateBeforeInstall"
  - AfterInstall: "LambdaFunctionToValidateAfterTraffic"
  - AfterAllowTestTraffic: "LambdaFunctionToValidateAfterTestTrafficStarts"
  - BeforeAllowTraffic: "LambdaFunctionToValidateBeforeAllowingProductionTraffic"
  - AfterAllowTraffic: "LambdaFunctionToValidateAfterAllowingProductionTraffic"
  ```
  - Example of an AppSpec file written in YAML for deploying a Lambda function
```
version: 0.0
Resources:
  - myLambdaFunction:
      Type: AWS::Lambda::Function
      Properties:
        Name: "myLambdaFunction"
        Alias: "myLambdaFunctionAlias"
        CurrentVersion: "1"
        TargetVersion: "2"
Hooks:
  - BeforeAllowTraffic: "LambdaFunctionToValidateBeforeTrafficShift"
  - AfterAllowTraffic: "LambdaFunctionToValidateAfterTrafficShift"
```
__RollBack__
- CodeDeploy rolls back deployments by redeploying a previously deployed revision of an application as a new deployment. 
- Deployments can be rolled back automatically or manually.

#### Code Pipeline 
   - Orchestrate the build, test and deployment as code changes
   - Automatically triggers pipeline on code changes
   - Integrate with AWS like code build,code deploy, cloudformation, ECS,Elastic Beanstalk & 3rd party tools    like jenkins, github 
   - Artifacts: Artifacts are passed, stored in Amazon S3 and then passed on to the next stage.
   - Stages: Stage examples would be build, test, deploy, load test etc. Each stage can have sequential actions and or parallel actions.

### X-Ray

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture.

AWS X-Ray supports applications running on:
- Amazon Elastic Compute Cloud (Amazon EC2).
- Amazon EC2 Container Service (Amazon ECS).
- AWS Lambda.
- AWS Elastic Beanstalk

- Linux system must run the X-Ray daemon. X-ray integration enabled for lambda. ECS/EKS runs x-ray container.
- AWS X-Ray supports tracing for applications that are written in Node.js, Java, and .NET. Code must be instrumented to use the AWS X-Ray SDK.
- The X-Ray SDK is installed in your application and forwards to the X-Ray daemon which forwards to the X-Ray API.You can then visualize what is happening in the X-Ray console.

__Key X-Ray Terminology__

- Trace: An X-Ray trace is a set of data points that share the same trace ID.
- Segments: An X-Ray segment encapsulates all the data points for a single component of the distributed application
- Subsegments: Subsegments provide more granular timing information and details about downstream calls that your application made to fulfill the original request.
- Annotations: An X-Ray annotation is system-defined or user-defined data associated with a segment. System-defined annotations include data added to the segment by AWS services, whereas user-defined annotations are metadata added to a segment by a developer
- Sampling: To provide a performant and cost-effective experience, X-Ray does not collect data for every request that is sent to an application. Instead, it collects data for a statistically significant number of requests.
- Metadata: Key / value pairs, not indexed and not used for searching.

__Tip: Remember that annotations can be used for adding system or user-defined data to segments and subsegments that you want to index for search. Metadata is not indexed and cannot be used for searching.__


### CloudFormation

- Yaml or Json template to provision your AWS resources
- You upload it to S3 and cloudformation runs API in template on your behalf
- Creates Stack and if fails rollback automatically

- CF template
  - __AWSTemplateFormatVersion__ section *(optional)* identifies the capabilities of the template. The latest template format version is 2010-09-09 and is currently the only valid value.
  - __Parameters__ - input custom values.
```
 Parameters: 
  InstanceTypeParameter: 
    Type: String
    Default: t2.micro
    AllowedValues: 
      - t2.micro
      - m1.small
      - m1.large
    Description: Enter t2.micro, m1.small, or m1.large. Default is t2.micro.
```
  - __Conditions__ - Control the creation of resources based on a condition. Applied to resources and outputs.
```
Conditions: 
  CreateProdResources: !Equals [ !Ref EnvType, prod ]
```
  - __Resources* ( Mandatory )__ - create AWS resources
```
  Resources:
   MyEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: "ami-0ff8a91507f77f867"
```
  - __Mappings__ - create custom mapping e.g. region:AMI. Need to know the values in advance.
```
  RegionMap: 
    us-east-1:
      HVM64: ami-0ff8a91507f77f867
      HVMG2: ami-0a584ac55a7631c0c
    us-west-1:
      HVM64: ami-0bdb828fd58c52235
      HVMG2: ami-066ee5fd4a9ef77f1
```
  - __Transforms__ - ref code located in S3 e.g. lambda code or reusable snippet of cf code
```
Transform: AWS::Serverless-2016-10-31
Resources:
  MyServerlessFunctionLogicalID:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      Runtime: nodejs8.10
      CodeUri: 's3://testBucket/mySourceCode.zip'
```
  - __Outputs__ - output values that you can import into other stacks.or view on the AWS CloudFormation console
```
Outputs:
  StackVPC:
    Description: The ID of the VPC
    Value: !Ref MyVPC
    Export:
      Name: !Sub "${AWS::StackName}-VPCID"
```

#### Cloudformation Nested Stacks

- allow to re-use of CF code for common use cases
- Basically ref a cf template from another cf 
```
Resources:
 Type: AWS::CloudFormation::Stack
 Properties:
   TemplateUrl: https://s3.amazonaws.com/../template.yml
```
#### CF APIs

- Creating a Stack - create-stack
- Desc & listing Stack - list-stacks & describe-stacks
- Listing Resources - list-stack-resources
- Deleting a Stack - delete-stack

#### Intrinsic Functions

__Note:__ You can use intrinsic functions only in specific parts of a template. Currently, you can use intrinsic functions in resource properties, outputs, metadata attributes, and update policy attributes. You can also use intrinsic functions to conditionally create stack resources.

__Ref__

- Fn::Ref (or !Ref in YAML),
- The intrinsic function Ref returns the value of the specified parameter or resource.
```
MyEIP:
  Type: "AWS::EC2::EIP"
  Properties:
    InstanceId: !Ref MyEC2Instance
```

__Fn::GetAtt__

- The Fn::GetAtt intrinsic function returns the value of an attribute from a resource in the template.
- Full syntax (YAML): Fn::GetAtt: [ logicalNameOfResource, attributeName ]
- Short form (YAML): !GetAtt logicalNameOfResource.attributeName

```
AWSTemplateFormatVersion: 2010-09-09
Resources:
  myELB:
    Type: AWS::ElasticLoadBalancing::LoadBalancer
    Properties:
      AvailabilityZones:
        - eu-west-1a
      Listeners:
        - LoadBalancerPort: '80'
          InstancePort: '80'
          Protocol: HTTP
  myELBIngressGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: ELB ingress group
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '80'
          ToPort: '80'
          SourceSecurityGroupOwnerId: !GetAtt myELB.SourceSecurityGroup.OwnerAlias
          SourceSecurityGroupName: !GetAtt myELB.SourceSecurityGroup.GroupName
```

__Fn::FindInMap__

- The intrinsic function Fn::FindInMap returns the value corresponding to keys in a two-level map that is declared in the Mappings section.
- Full syntax (YAML): Fn::FindInMap: [ MapName, TopLevelKey, SecondLevelKey ]
- Short form (YAML): !FindInMap [ MapName, TopLevelKey, SecondLevelKey ]

```
Mappings: 
  RegionMap: 
    us-east-1: 
      HVM64: "ami-0ff8a91507f77f867"
      HVMG2: "ami-0a584ac55a7631c0c"
    us-west-1: 
      HVM64: "ami-0bdb828fd58c52235"
      HVMG2: "ami-066ee5fd4a9ef77f1"
Resources: 
  myEC2Instance: 
    Type: "AWS::EC2::Instance"
    Properties: 
      ImageId: !FindInMap
        - RegionMap
        - !Ref 'AWS::Region'
        - HVM64
      InstanceType: m1.small
```

__Fn::ImportValue__

- The intrinsic function Fn::ImportValue returns the value of an output exported by another stack.
- You typically use this function to create cross-stack references.

```
Fn::ImportValue:
  !Sub "${NetworkStackName}-SecurityGroupID"
```

__Fn::Join__

- Full syntax (YAML): Fn::Join: [ delimiter, [ comma-delimited list of values ] ]
- Short form (YAML): !Join [ delimiter, [ comma-delimited list of values ] ]

```
!Join
  - ''
  - - 'arn:'
    - !Ref Partition
    - ':s3:::elasticbeanstalk-*-'
    - !Ref 'AWS::AccountId'
```

__Fn::Sub__

- The intrinsic function Fn::Sub substitutes variables in an input string with values that you specify.
- In your templates, you can use this function to construct commands or outputs that include values that aren’t available until you create or update a stack.

```
Name: !Sub
  - www.${Domain}
  - { Domain: !Ref RootDomainName }
```