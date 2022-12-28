# Creates ECS Ec2 Cluster 

* VPC
* 2 Public subnets in 2 different AZs
* Internet Gateway
* Routing tables

Commands:  


```bash
aws configure
```

```bash
pip3 install cfn-lint
```

```bash
cfn-lint vpc.yml
```

```bash
cfn-lint ecs-ec2-cfn.yml
```

```bash
cfn-lint create_IAM_roles.yml
```

```bash
aws cloudformation create-stack --capabilities CAPABILITY_NAMED_IAM --stack-name ecs-iam  --template-body file://./create_IAM_roles.yml --profile <profile_name>
```

> creates four roles with policies

![image](https://user-images.githubusercontent.com/66196388/184866623-18d7b2aa-9bcc-4b23-b77b-3c6d5c1e66b5.png)


```bash
aws cloudformation create-stack --stack-name ecs-vpc --template-body file://./vpc.yml --profile <profile_name>
```

```bash
aws cloudformation create-stack --stack-name ecs-ec2-task  --template-body file://./ecs-ec2-cfn.yml --profile <profile_name>
```

```bash
aws cloudformation update-stack --stack-name ecs-vpc --template-body file://./vpc.yml
```

```bash
aws cloudformation update-stack --stack-name ecs-ec2-task --template-body file://./ecs-ec2-cfn.yml
```

```bash
aws cloudformation update-stack --stack-name ecs-iam --template-body file://./create_IAM_roles.yml
```

```bash
aws cloudformation delete-stack --stack-name aws-cfn && aws cloudformation delete-stack --stack-name ecs-ec2-cfn.yml
```


## Image

![image](https://user-images.githubusercontent.com/66196388/183415024-b7bca886-f6be-4487-8101-72c839380924.png)
