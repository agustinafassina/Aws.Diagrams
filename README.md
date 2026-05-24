# ☁️ Aws Solutions
Reference **AWS architectures and short guides**: diagrams, decision tables, and notes per topic—one folder each. Not a replacement for [AWS documentation](https://docs.aws.amazon.com/); no deployment code here unless a README links to an external scripts repo.

**How to use:** open a folder → read its `README` → use the diagram or tables in reviews and onboarding.

### 📚 Index
| | Folder | Summary |
| --- | --- | --- |
| 🏗️ | [`complete-infrastructure/`](./complete-infrastructure/) | ALB, WAF, ECS/Docker, ECR, path routing, CloudWatch, CloudTrail, S3 logging. |
| 🛡️ | [`complete-infra-with-services-security/`](./complete-infra-with-services-security/) | Security layers (Shield, GuardDuty, WAF, Inspector, Macie, Config, Security Hub) + service ↔ control matrix. |
| 🌐 | [`gateway/`](./gateway/) | Domain → API Gateway → ALB → ECS (optional EC2 targets). |
| 🖥️ | [`ec2-bastion-and-private-rds/`](./ec2-bastion-and-private-rds/) | Private RDS, app on EC2/Docker, bastion + SSH tunnel for developers. |
| 🍃 | [`ec2-mongodb-s3-backups/`](./ec2-mongodb-s3-backups/) | MongoDB on EC2 vs DocumentDB; backups to S3 — scripts in [Aws.Ec2.MongoDB.WithBackups.S3](https://github.com/agustinafassina/Aws.Ec2.MongoDB.WithBackups.S3). |
| 🗄️ | [`rds-vs-aurora-vs-dynamodb/`](./rds-vs-aurora-vs-dynamodb/) | When to use RDS, Aurora, or DynamoDB (decision tables). |
| 🔐 | [`password-policies-iam/`](./password-policies-iam/) | IAM password policy, rotation, MFA, Access Analyzer. |

**Convention:** each folder has a `README.md` and, when applicable, a diagram (`diagram.jpg` / `diagram.png`). Add a row here when you add a new top-level folder.

### 🛠️ Diagram tools
[AWS Architecture Icons](https://aws.amazon.com/architecture/icons/) · [draw.io](https://www.diagrams.net/) · Lucidchart · Miro

### 📄 License
Images are for personal use. AWS icons and marks: [AWS Trademark Guidelines](https://aws.amazon.com/legal/trademark-guidelines/).