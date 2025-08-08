# Summary of Relevant Options for CCE Challenge

## Choice of DynamoDB
- **Reason**: DynamoDB was selected as the datastore because it is a serverless, fully managed NoSQL database that aligns with the team's preference for high-abstraction AWS services. It is compatible with the AWS Free Tier (25 GB storage, 25 read/write capacity units) and scales automatically, reducing maintenance overhead compared to alternatives like RDS or self-managed databases.
- **Impact**: Ensures cost-efficiency and simplicity for the challenge, with fast writes for JSON data.

## Choice of CloudFormation
- **Reason**: CloudFormation was chosen as the infrastructure-as-code tool, as requested, to define the AWS resources declaratively. Splitting the template into modular files (dynamodb.yaml, lambda.yaml, api_gateway.yaml, iam_roles.yaml) improves maintainability and readability compared to a single monolithic template.
- **Impact**: Facilitates debugging, updates, and collaboration, while adhering to the team's tech stack.

## Choice of Python
- **Reason**: Python was used for the Lambda function due to its simplicity, widespread use, and alignment with the challenge's preference. It integrates well with AWS SDK (boto3) for DynamoDB operations.
- **Impact**: Simplifies development and testing, with a large ecosystem of tools (e.g., pylint, pytest) for CI/CD.

## Choice of GitHub Actions for CI/CD
- **Reason**: GitHub Actions was selected for CI/CD due to its native integration with GitHub, flexibility, and support for AWS CLI, SonarQube, and Artifactory integrations. It supports automated linting, testing, validation, and deployment.
- **Impact**: Streamlines the pipeline, reduces setup complexity, and leverages modern CI/CD practices.

## Modular Template Design
- **Reason**: Splitting the CloudFormation template into multiple files allows each component (DynamoDB, Lambda, API Gateway, IAM) to be managed independently, making it easier to update or reuse specific parts.
- **Impact**: Enhances maintainability and aligns with best practices for infrastructure as code.

## Free Tier Compatibility
- **Reason**: All services (Lambda, API Gateway, DynamoDB) were chosen to stay within AWS Free Tier limits (1M Lambda invocations, 1M API Gateway calls, 25 GB DynamoDB storage). The solution avoids unnecessary resources to minimize costs.
- **Impact**: Ensures the solution is cost-free for testing and demonstration purposes, with clear cleanup instructions.

## Conclusion
The solution prioritizes simplicity, maintainability, and alignment with the CCE team's requirements. DynamoDB and CloudFormation provide a serverless, high-abstraction foundation, while Python and GitHub Actions enable robust development and deployment workflows. The modular design and Free Tier compatibility make the solution practical and efficient.