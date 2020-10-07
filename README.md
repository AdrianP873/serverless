# Serverless application pipeline
CodePipeline does not currently support deploying Lambda functions with CodeDeploy. We can workaround this limitation by leveraging the Serverless Application Model to deploy code changes to your Lambda functions with a Canary deployment strategy.
 
## Infrastructure Deployment
The infra directory contains a CloudFormation template (build-pipeline.yaml) which provisions a CICD pipeline that connects to this GitHub source repository. In the case of real world usage, this template should be separated from the application repo.

The build stage packages up the serverless function and outputs an artifact to an S3 bucket.

The deploy stage generates a change set for the serverless CloudFormation stack. Upon manual approval, another version of the lamba function is provisioned with the updated application code and traffic is gradually shifted to the updated Lambda function via a Canary deployment strategy.

The pipeline is triggered upon any commits made to this repo.
