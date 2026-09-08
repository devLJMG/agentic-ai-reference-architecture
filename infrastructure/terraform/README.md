# Terraform infrastructure

This directory will contain the deployable AWS infrastructure for the reference architecture.

Planned modules:

- networking: VPC, private subnets, routing and endpoints;
- identity: Amazon Cognito resources;
- agent runtime and gateway resources;
- retrieval: S3 and knowledge-base dependencies;
- observability: CloudWatch logs, metrics and alarms;
- IAM: least-privilege execution roles and policies.

No production credentials, account IDs or secrets should be committed to this repository.
