# CodePipeline Template

This repository is a template for applications deployed with CodePipeline -> CodeBuild -> CloudFormation


### GitHub -> AWS CodeStar Authentication Setup

1. [Create a Connection](https://docs.aws.amazon.com/dtconsole/latest/userguide/connections-create.html) for the supported external Git platform in the AWS Region you plan to use it
2. [Create an SSM Parameter](https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-create-console.html) in the same region, whose value is the ARN of the Connection as a String
3. Place the parameter in a Parameter Namespace that makes sense when viewing in the console, e.g. /GitHubConnectionArn/<connection-name> for a GitHub connection
4. Replace any reference in `/build/template.yml` to `MY_CONNECTION_NAME` to the name of the SSM Parameter

### Initial Deployment

1. Authenticate to desired AWS Account with Administrator Access in your bash shell
2. Navigate to root directory of this repository
4. Run `./init` and fill in the requested information
5. Watch CloudFormation console for progress deploying initial stack (`/build/template.yml`)
6. Watch CodePipeline console for progress of first pipeline run & monitor CodeBuild + CloudFormation progress
7. Commit + Push changes to branch in order to trigger a new build

### Application Destruction (Currently Manual)

1. Delete any objects from S3 Buckets
2. Delete any ECR Container Images
3. Delete any Manual Route53 Records (e.g. ACM certificiate verification CNAMEs)
4. Delete the CloudFormation Stack for the deployment

### Notes

* CodeBuild + CodePipeline + CloudFormation IAM Roles are currently overprivileged and should be scoped better 
* Load Balancer should be configured to make a better HA ECS deployment
* Load Balancer could be added as an origin behind CloudFront + Route53 Config
* Many other potential improvements in mind, like blue-green deployments.
