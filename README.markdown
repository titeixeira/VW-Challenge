# CCE Technical Challenge - CloudFormation (Modular)

## Overview
This project implements an AWS-based solution for the CCE technical challenge using modular CloudFormation templates. It includes:
- An API endpoint to receive JSON data and store it in DynamoDB.
- Infrastructure defined using AWS CloudFormation in YAML, split into multiple templates.

## Prerequisites
- AWS account with Free Tier eligibility.
- AWS CLI installed and configured with credentials.
- (Optional) `curl` or Postman for testing the API.

## Setup
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd cce-challenge
   ```
2. Ensure AWS CLI is configured:
   ```bash
   aws configure
   ```

## Deployment
1. Upload modular templates to an S3 bucket (or use local paths if deploying locally):
   ```bash
   aws s3 cp dynamodb.yaml s3://<your-bucket>/templates/
   aws s3 cp lambda.yaml s3://<your-bucket>/templates/
   aws s3 cp api_gateway.yaml s3://<your-bucket>/templates/
   aws s3 cp iam_roles.yaml s3://<your-bucket>/templates/
   ```
2. Update `master.yaml` with the correct S3 URLs for `TemplateURL`.
3. Validate the master template:
   ```bash
   aws cloudformation validate-template --template-body file://master.yaml
   ```
4. Deploy the stack:
   ```bash
   aws cloudformation deploy --template-file master.yaml --stack-name CceChallengeStack --capabilities CAPABILITY_IAM
   ```
5. Note the API endpoint URL from the stack outputs:
   ```bash
   aws cloudformation describe-stacks --stack-name CceChallengeStack --query "Stacks[0].Outputs"
   ```

## Testing
- Send a POST request to the API endpoint with a JSON body:
  ```bash
  curl -X POST <api-endpoint> -H "Content-Type: application/json" -d '{"name": "example", "value": 123}'
  ```
- Check DynamoDB for stored items:
  - AWS Console: DynamoDB > Tables > DataTable > Explore items.
- Check logs in CloudWatch:
  - CloudWatch > Log Groups > /aws/lambda/StoreDataFunction.

## Cleanup
To avoid charges, delete the stack:
```bash
aws cloudformation delete-stack --stack-name CceChallengeStack
aws cloudformation wait stack-delete-complete --stack-name CceChallengeStack
```