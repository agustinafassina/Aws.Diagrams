# Aws.Architecture
A reference repository for **architecture and solutions on Amazon Web Services (AWS)**: exported diagrams, cloud design patterns, **databases**, **best practices**, and complementary material added over time.

It started as a **diagram** collection (regional views, security, and services); the goal is to **grow** into short guides, design notes, checklists, and other resources useful for teams building on AWS—without replacing the official AWS documentation.

## Current contents
### Diagrams
Each topic lives in **its own folder** with a **README** (what the drawing shows, link to the image, and any tables or notes). Images are typically JPG, PNG, or SVG depending on the tool.
| Folder | Diagram | README |
| ------ | ------- | ------ |
| [`complete-infrastructure/`](./complete-infrastructure/) | [`infrastructure-aws.jpg`](./complete-infrastructure/infrastructure-aws.jpg) | [README](./complete-infrastructure/README.md) — ALB, WAF, ECS/Docker, ECR, path-based routing (`/api`, `/api/v2`), CloudWatch, CloudTrail, S3 logging. |
| [`complete-infra-with-services-security/`](./complete-infra-with-services-security/) | [`infrastructure-security-aws.jpg`](./complete-infra-with-services-security/infrastructure-security-aws.jpg) | [README](./complete-infra-with-services-security/README.md) — layered security (Shield, GuardDuty, WAF, Inspector, Macie, Config, Security Hub, etc.) and a **service ↔ control** matrix. |

#### Previews

**[Complete AWS infrastructure](./complete-infrastructure/README.md)**  
![Complete AWS infrastructure](./complete-infrastructure/infrastructure-aws.jpg)

**[Infrastructure + security services](./complete-infra-with-services-security/README.md)**  
![Infrastructure and security on AWS](./complete-infra-with-services-security/infrastructure-security-aws.jpg)

## Planned additions
- **Cloud solutions on AWS:** high availability patterns, multi-account setups, networking, observability, cost awareness.
- **Databases:** RDS vs. serverless choices, DynamoDB, backups, migrations, and architecture-oriented summaries.
- **Best practices:** security, operations, naming, tagging, checklist-style reviews.
- **More diagrams** using the same folder-per-topic and README convention.

Today the main focus remains **diagrams and documentation beside them**; deployment code and IaC are not required for this repository—only what helps architectural clarity.

## Suggested conventions
- **One folder per diagram (or family):** keep the image, a `README.md`, and any variants together—same pattern as the folders above.
- **Clear names:** include context (environment, region, or purpose) and, when useful, `simple` / `complete` or a version in the filename, for example `prod-multi-az-v2.jpg`.
- **Format:** JPG or PNG for exports; SVG when your tool supports it and you want lossless scaling.
- **As the repo grows:** optional subfolders by domain (`network/`, `data/`, `observability/`, `best-practices/`, etc.).

Update this root README when you add a new top-level folder, or link straight to files from the repository tree.

## Common tools
Diagrams are often built with [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/), [draw.io / diagrams.net](https://www.diagrams.net/), Lucidchart, Miro, or other tools that work with the official AWS icons.

## License
Images are for personal use. AWS icons and marks are subject to the [AWS Trademark Guidelines](https://aws.amazon.com/legal/trademark-guidelines/).
