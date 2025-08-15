# AWS-Day-20-Soc2-evidence

Day 20: Automated SOC 2 Compliance Evidence Collection

Overview
Enterprise-grade serverless solution for automated SOC 2 Type II compliance evidence collection from AWS services. Built for banking clients requiring continuous audit readiness.

Architecture
EventBridge Scheduler (Daily) → Lambda (Python 3.13) → Multiple AWS Services → S3 (Encrypted Storage)
                                        ↓
                          CloudTrail, Config, GuardDuty, IAM, S3, VPC

Services Monitored
1.	CloudTrail: Logging status and 24h event counts
2.	AWS Config: Compliance rule summaries
3.	GuardDuty: Security findings by severity
4.	IAM: Password age and unused access keys
5.	S3: Bucket encryption status
6.	VPC Security Groups: Open access detection

Key Features
1.	Automated Daily Collection: EventBridge Scheduler triggers Lambda
2.	Secure Storage: S3 with versioning and lifecycle policies
3.	Dual Output: JSON data + human-readable Markdown reports
4.	Enterprise Ready: Least-privilege IAM roles
5.	Cost Optimized: Glacier transition @ 30 days, deletion @ 365 days

Deployment
Prerequisites
1.	AWS Account with appropriate permissions
2.	AWS CLI configured (optional)

Step 1: Create S3 Bucket
Create bucket with versioning and lifecycle policy

Step 2: Deploy Lambda Function
1.	Create IAM role with provided policy
2.	Upload lambda_function.py
3.	Set environment variables: 
o	EVIDENCE_BUCKET: Your S3 bucket name
o	EVIDENCE_PREFIX: evidence

Step 3: Schedule Execution
Create EventBridge Scheduler rule:
1.	Rate: rate(1 day)
2.	Target: Lambda function

Sample Output
Evidence files generated daily in S3:
evidence/
└── 2025/08/15/143022/
    ├── evidence.json          # Raw compliance data
    └── report.md             # Human-readable report

Security Considerations
1.	Least Privilege: IAM role grants minimum required permissions
2.	Encryption: S3 server-side encryption enabled
3.	Versioning: S3 object versioning for audit trail
4.	Lifecycle: Automated archival and deletion policies

Business Value
Enables enterprise clients to demonstrate continuous SOC 2 Type II compliance with:
1.	Automated evidence collection
2.	Timestamped audit trails
3.	Cost-effective long-term storage
4.	Ready-to-present compliance reports

Technologies Used
1.	AWS Lambda (Python 3.13)
2.	Amazon EventBridge Scheduler
3.	Amazon S3 (with lifecycle policies)
4.	AWS IAM (least-privilege roles)
5.	Multiple AWS APIs (CloudTrail, Config, GuardDuty, etc.)


Part of 100 Days of Cloud challenge - Day 20
