# 🔐 IAM password policies, rotation, and MFA

Guide for hardening **human IAM users** in an AWS account: a strong **account password policy**, regular **rotation**, and **multi-factor authentication (MFA)**. Together they reduce credential theft and weak-password risk for console and programmatic workflows that still rely on IAM users.

> **Scope:** This folder documents **IAM account password policy** and related controls. **MFA** is not configured inside the password policy—it is enforced per user (or via permission boundaries / SCPs). **IAM Identity Center (SSO)** uses its own session and IdP policies when you federate users instead of long-lived IAM users.

## 🎯 Goals

| Goal | Control |
| --- | --- |
| Strong passwords | Account password policy (length, character classes) |
| Limited password lifetime | **Maximum password age** (expiration) |
| No password recycling | **Password reuse prevention** (history) |
| Fewer shared / stale secrets | Rotation + **users change own password** where appropriate |
| Stolen password not enough to sign in | **MFA** on IAM users (and prefer SSO over many IAM users) |
| Ongoing access review | **IAM Access Analyzer**, credential reports, least privilege |

## 📋 IAM account password policy

The **account password policy** applies to **IAM users** who have a console password. It is **one policy per account** (not per user). Set it in **IAM → Account settings → Password policy**, or with the API/CLI (`UpdateAccountPasswordPolicy`).

### Typical settings

| Setting | Recommendation | Notes |
| --- | --- | --- |
| **Minimum password length** | 14+ (or org standard) | Longer passwords resist brute force better than complexity alone. |
| **Require uppercase / lowercase** | ✅ | Part of character-class rules. |
| **Require numbers** | ✅ | |
| **Require symbols** | ✅ | Non-alphanumeric characters. |
| **Allow users to change their own password** | ✅ | Needed for self-service rotation unless you only use admin resets. |
| **Enable password expiration** | ✅ | Set **maximum password age** (for example **90 days**). |
| **Password expiration requires administrator reset** | Optional | If enabled, users cannot remove expiry themselves after it is required—stricter, more admin overhead. |
| **Prevent password reuse** | ✅ | Remember **24** previous passwords (AWS maximum for history). |

### 🔁 Rotation (expiration)

- **Maximum password age** forces users to set a new password after N days (common values: **60–90** days; align with your compliance framework).
- Users see prompts in the **AWS Management Console** when the password is about to expire or has expired.
- **Service accounts** should **not** use console passwords; use **IAM roles** and short-lived credentials instead so rotation policy applies only to people.
- Pair expiration with **password history** so users cannot rotate back to an old password.

### Example: CLI

```bash
aws iam update-account-password-policy \
  --minimum-password-length 14 \
  --require-uppercase-characters \
  --require-lowercase-characters \
  --require-numbers \
  --require-symbols \
  --allow-users-to-change-password \
  --max-password-age 90 \
  --password-reuse-prevention 24
```

### Example: CloudFormation (snippet)

```yaml
AccountPasswordPolicy:
  Type: AWS::IAM::AccountPasswordPolicy
  Properties:
    MinimumPasswordLength: 14
    RequireUppercaseCharacters: true
    RequireLowercaseCharacters: true
    RequireNumbers: true
    RequireSymbols: true
    AllowUsersToChangePassword: true
    MaxPasswordAge: 90
    PasswordReusePrevention: 24
```

## 🔑 MFA (separate from password policy)

**MFA is mandatory for production accounts** where IAM users can sign in to the console or use sensitive API calls. Configure it per user under **IAM → Users → Security credentials → Assign MFA device**.

| MFA type | Use case |
| --- | --- |
| **Virtual MFA** (app) | Default for most users (Authenticator, etc.). |
| **Hardware MFA** / **FIDO security key** | Higher assurance, phishing-resistant options where supported. |

**Enforcement patterns:**

- **IAM policy** on users/groups: deny sensitive actions unless `aws:MultiFactorAuthPresent` is `true` (and tighten with `aws:MultiFactorAuthAge` for recent MFA).
- **AWS Organizations SCPs** to require MFA account-wide where applicable.
- **Prefer IAM Identity Center** with your corporate IdP and MFA at the IdP layer instead of many long-lived IAM users.

Example condition (illustrative—adapt actions to your needs):

```json
"Condition": {
  "BoolIfExists": {
    "aws:MultiFactorAuthPresent": "true"
  }
}
```

## 🔍 Related IAM security practices

- **🔎 IAM Access Analyzer:** find resources shared externally and validate intended access; run periodically and on changes.
- **📊 Credential report:** download **IAM credential report** to find users without MFA, old passwords, or unused access keys.
- **🚫 Access keys:** disable console password for users that only need API access via roles; rotate keys on a schedule if keys are unavoidable.
- **👤 Least privilege:** attach policies to **groups**; avoid inline policies except exceptions; use **permission boundaries** for power users.
- **🏢 SSO:** for teams, use **IAM Identity Center** instead of proliferating IAM users with passwords.

## 📚 AWS documentation
- [Setting an account password policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html)
- [Managing passwords for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords.html)
- [Using multi-factor authentication (MFA) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)
- [IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html)
