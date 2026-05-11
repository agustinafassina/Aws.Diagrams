# Complete infrastructure with security services in Aws
This AWS security setup covers DNS protection, network visibility, web application filtering, container and instance vulnerability scanning, storage protection, centralized logging, configuration auditing, and security posture management. It combines services such as Route 53 Query Logging, AWS Shield, VPC Flow Logs, GuardDuty, Network Firewall, WAF, Inspector, ECR scanning, S3 Block Public Access, Macie, CloudTrail, AWS Config, Security Hub, CloudWatch Alarms, IAM, KMS, and Secrets Manager to provide layered security across the entire infrastructure.

## Diagram
- [`infrastructure-aws.jpg`](./infrastructure-security-aws.jpg) — AWS infrastructure diagram.

### Aws Services
| Component                 | Recommended Security Service                 | Purpose                                                      | Where Logs Are Stored                          | Where They Are Viewed                                 |
| ------------------------- | -------------------------------------------- | ------------------------------------------------------------ | ---------------------------------------------- | ----------------------------------------------------- |
| Route 53                  | Route 53 Query Logging + AWS Shield          | DNS auditing and DDoS protection.                            | CloudWatch Logs / Shield internal telemetry.   | CloudWatch Logs / Shield console.                     |
| VPC                       | VPC Flow Logs + GuardDuty + Network Firewall | Network visibility, threat detection, and traffic filtering. | CloudWatch Logs or S3.                         | CloudWatch Logs, GuardDuty, Network Firewall console. |
| Application Load Balancer | AWS WAF + AWS Shield                         | Web traffic protection and DDoS mitigation.                  | S3, CloudWatch Logs, or Firehose for WAF logs. | WAF console, CloudWatch, S3, Security Hub.            |
| ECS / Docker              | Amazon Inspector                             | Vulnerability detection for containers and workloads.        | Inspector findings store.                      | Inspector console, Security Hub.                      |
| ECR                       | ECR Image Scanning                           | Vulnerability scanning for container images.                 | ECR scan findings.                             | ECR console, Security Hub.                            |
| EC2                       | Amazon Inspector                             | Vulnerability detection for instances.                       | Inspector findings store.                      | Inspector console, Security Hub.                      |
| S3                        | S3 Block Public Access + Amazon Macie        | Prevents public exposure and detects sensitive data.         | Macie findings / CloudTrail / S3-related logs. | Macie, S3, CloudTrail, Security Hub.                  |
| CloudTrail                | CloudTrail Logs in S3 + AWS Config           | Audit trail and configuration tracking.                      | S3 and AWS Config history snapshots.           | CloudTrail console, AWS Config console, Athena.       |
| Account / Multi-service   | AWS Security Hub                             | Centralized security posture management.                     | Security Hub findings store.                   | Security Hub console.                                 |
| Observability             | CloudWatch Alarms                            | Security and operational alerting.                           | CloudWatch metric/alarm state.                 | CloudWatch console.                                   |
| Access Control            | IAM                                          | Permissions and role management.                             | Audited via CloudTrail.                        | IAM console, CloudTrail.                              |
| Encryption / Secrets      | KMS + Secrets Manager                        | Encryption and secure credential management.                 | Audited via CloudTrail.                        | KMS and Secrets Manager consoles, CloudTrail.         |
