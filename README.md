# This AWS Lambda function inspects the route tables of a specified VPC in your AWS account and identifies relationships between destination CIDR blocks for each route target—specifically, whether any CIDR is a subnet of another within the same target and route table.

# Features
Fetches all route tables associated with a given VPC.

Groups routes by route table and target (e.g., Gateway, NAT, Transit Gateway, etc.).

Analyzes CIDR blocks to detect subnet relationships.

Returns subnet relationship findings as a structured response.

# Use Case
This function is particularly useful for auditing and validating routing configurations in VPCs. It helps identify overlapping or nested routes that may lead to unexpected network behavior.

# Usage
# Event Input
The Lambda function expects an event with the following parameters:
"vpc_id": "vpc-xxxxxxxx",
  "region": "us-east-1" // optional, defaults to 'us-east-1'

  "statusCode": 200,
  "body": {
    "subnet_relationships": [
      "10.0.1.0/24 is a subnet of 10.0.0.0/16 (target: igw-abc123, route table: rtb-xyz789)"
    ]
  }
# Error Response

  "statusCode": 400,
  "body": "Missing required parameter: vpc_id"

# Deployment
This function is written in Python and designed for use as an AWS Lambda. You can deploy it using AWS SAM, CloudFormation, or directly through the AWS Console.

IAM Permissions Required
Ensure your Lambda role has the following permissions:


  "Effect": "Allow",
  "Action": [
    "ec2:DescribeRouteTables"
  ],
  "Resource": "*"
