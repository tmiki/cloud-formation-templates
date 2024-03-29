# cloud-formation-templates

# Overview
This repository provides sample Cloudformation templates.
Please note the following items.

- some templates depend on other template.
- some files need storing into an S3 bucket, and you have to put them in advance.

# Structure of Layers
## CloudFormation StackSets templates
As templates classified for using StackSets, their name start with "cfn-stack-set-" prefix and are stored in the "stack-sets/" directory.  

- cfn-stack-set-01-administrator-account.yml
- cfn-stack-set-01-target-account.yml
- cfn-stack-set-11-resources.yml

## Regular CloudFormation templates
All templates are mostly classified as follows, but there are some execptions.
Basically, bigger numbered templates depend on smaller numbered ones.

- 0x: Most basic templates needed by all other templates.
- 1x,2x: AWS resources dedicated to the application you built which don't require server-like resources. In other words, it does not needs the hourly fee.
- 3x,4x: AWS resources dedicated to the application which require server-like resources. If it is possible, you have to terminate them when you are not using to reduce cost.
- 5x,6x: RESERVED
- 7x,8x: RESERVED
- 9x: RESERVED

# How to run
This section shows example of AWS CLI commands and their options to create CloudFormation stacks.  
Please replace their parameters/options as they fit your environment.

## CloudFormation StackSets templates
TBD

## Regular CloudFormation templates

- cfn-01-basis.yml

```
$ aws --profile <your AWS CLI profile> cloudformation deploy \
  --template-file cfn-01-basis.yml \
  --stack-name <stack name> \
  --parameter-overrides \
    EnvName=dev1 \
    AppServiceName=<your app name> \
    IpAddressAllowedSsh=<global IP address(es) with prefix being allowed to connect to VPC via SSH> \
    EnableNatGw=false
```

- cfn-02-route53.yml

TBD

- cfn-03-acm.yml

TBD

- cfn-32-rds.yml

TBD


# Notes
## CloudFormation StackSets
TBD

## Regular CloudFormation templates
### ACM(Amazon Certificate Manager)
You have to create a global certificate in the North Virginia region in advance. That corresponds to the domain name of the environment you want to build.
Since Cloudformation cannot create AWS resources in other region, you cannot create a global certificate if you are intended to build an environment in other regions.

### API Gateway
The CloudFormation template to create an API Gateway instance requires items below.

1. needs a global certificate created in advance(as above).
2. an S3 bucket is created beforehand.
3. a Swagger template is stored in that S3 bucket as I mentioned above.


