# Serverless application pipeline
CodePipeline does not currently support deploying Lambda functions with CodeDeploy. We can workaround this limitation by leveraging the Serverless Application Model to deploy code changes to your Lambda functions with a Canary deployment strategy.
 
## Infrastructure Deployment
The infra directory contains a CloudFormation template (build-pipeline.yaml) which provisions a CICD pipeline that connects to this GitHub source repository.

The build stage packages up the serverless function and API Gateway, and outputs an artifact to an S3 bucket.

The deploy stage generates a change set for the serverless CloudFormation stack. Upon manual approval, the updated lamba function is provisioned and traffic is gradually shifted to the updated function via a Canary deployment strategy.

The pipeline is triggered upon any commits made to this repo.
