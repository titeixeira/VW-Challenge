# CCE Technical Challenge - CloudFormation (Modular)
This is my first attempt to implement a CI/CD pipeline for a CloudFormation stack.
Never tried before, so it's a bit of a challenge. Hope you liked at least the code.
Of course I could improve the stackset to be only a single template, but I preferred to keep it modular to be easy to me in order to troubleshoot and debug.
This challenge took me 4 hours to do it at the point it was due.

## Overview
This project implements an AWS-based solution for the CCE technical challenge using modular CloudFormation templates. It includes:
- An API endpoint to receive JSON data and store it in DynamoDB.
- Infrastructure defined using AWS CloudFormation in YAML, split into multiple templates.

## Prerequisites
- AWS account with Free Tier eligibility.
- (Optional) `curl` or Postman for testing the API.

## Setup
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd cce-challenge
   ```

## Deployment
1. In a AWS account, go to CloudFormation Service and select create Stack
2. Start with the dynamodb.yaml
3. Then the iam_roles.yaml and give the parameters given by the dynamodb.yaml Output
4. Then the lambda.yaml and give the parameters given by the dynamodb.yaml Output
5. Then the api_gateway.yaml and give the parameters given by the lambda.yaml Output   

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
To avoid charges, delete the stacks

## CI/CD
The CI/CD pipeline is defined in the ci-cd.yaml file. It includes the following steps, but didn't tested yet.
1. Checkout code
2. Set up Python
3. Install dependencies
4. Run pylint
5. Run tests
6. SonarQube Scan
7. Configure AWS credentials
8. Validate CloudFormation templates
9. Upload to Artifactory
10. Deploy to AWS
11. Notify Slack
