# Secrets Scan

This workshop module focuses on identifying and preventing the exposure of sensitive credentials, API keys, and other secrets in source code, configuration files, and git history.

## Why is Secrets Scan Important?
This is an old problem, but it is still a common one ([especially with the AI surge](https://www.wiz.io/blog/leaking-ai-secrets-in-public-code)). Secrets are the keys to your kingdom. If a password or token is accidentally committed to code, it's immediately at risk, potentially leading to:

- **Data Breaches** - Exposed credentials can lead to unauthorized access
- **Access to our Systems** - Compromised secrets enable lateral movement
- **Supply Chain Attacks** - Compromised release artifacts

All of this can lead to:

- **Compliance Issues** - Regulatory requirements for data protection
- **Financial Loss** - Unauthorized usage of cloud services
- **Reputation Damage** - Public exposure of security incidents

Secrets scan involves scanning code repositories, commit history, and configuration files to identify exposed credentials such as API keys, passwords, tokens, certificates, and other sensitive information that should not be stored in version control.

> [!TIP]
> Ideally, we should implement this before pushing the code to the repository, using [pre-commit](https://github.com/pre-commit/pre-commit) or similar tools. But accidents happen, so it's important to have a process to detect them in the pipeline as a safety net.

### Common Types of Secrets

#### **Generic Credentials**
- Hard-coded passwords, database connection strings, custom tokens, plaintext encryption keys
- 58% of all detected secrets [^1]
#### **Database Service Credentials**
- MongoDB connection strings, MySQL/PostgreSQL credentials
- 19% of public-repo leaks are MongoDB alone [^2]
#### **Cloud Provider Keys**
- AWS IAM access keys, Google Cloud keys, Azure SAS tokens
- AWS keys represent 8% of private-repo leaks [^2]
#### **Third-Party API Keys**
- Google API, Stripe, Twilio, SendGrid, OpenWeatherMap tokens
- OpenWeatherMap tokens among top 10 leaked services [^3]
#### **Messaging/Bot Tokens**
- Telegram Bot tokens, Slack/Discord webhooks
- Telegram Bot tokens account for 6.3% of public leaks [^1]
#### **Gen-AI Service Keys**
- OpenAI, HuggingFace, Gemini, Pinecone API keys
- OpenAI key leaks grew 1,212× year-over-year [^4]
#### **Private Cryptographic Material**
- RSA/SSH private keys, JWT signing keys, TLS certificates
- RSA private keys consistently rank in top-10 leak types
#### **OAuth/Personal Access Tokens**
- GitHub PATs, GitLab tokens
- Detected hundreds of times daily, classified as "highly critical" in 41% of cases [^4]

### Other types of secrets or sensitive data
There are other types of secrets or sensitive data that may not be covered by the tools we will use in this workshop, but that are still important to keep in mind:

#### **Webhooks**
- Webhooks are used to trigger actions in other systems, and can be used to trigger malicious actions.
  - Like Slack webhooks, that can be used to impersonate a user and send messages to a channel.
#### **AWS Account IDs**
- AWS account IDs (or other cloud provider identifiers) can be used to enumerate resources and help attackers to map the attack surface.
  - There's a lot of discussion about if this should be considered a secret or not. [According to AWS they are not](https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-identifiers.html), but we think this article from Daniel Grzelak is a good explanation of why they are: [The Final Answer: AWS Account IDs Are Secrets](https://www.plerion.com/blog/the-final-answer-aws-account-ids-are-secrets)
#### **Internal Documents or PII**
- PDFs, log files, customer data dumps, identity scans and even bank statements that slip into repos during troubleshooting or demo work.

## Tools Used in This Module

- [**TruffleHog**](https://github.com/trufflesecurity/trufflehog) - Git history secrets scanner that finds credentials, API keys, and other secrets
- [**Gitleaks**](https://github.com/gitleaks/gitleaks) - Git history and filesystem secrets scanner for detecting hardcoded secrets

## Learning Objectives

By the end of this module, you will:
- Understand different types of secrets and their risks
- Learn to use automated secrets detection tools
- Know how to scan git history for leaked credentials
- Learn to prevent future secret exposures

## Security Checklist

- [ ] Use environment variables for secrets
- [ ] Implement proper .gitignore patterns
- [ ] No secrets in source code
- [ ] Git history cleaned of secrets
- [ ] Environment variables properly configured
- [ ] Secrets management solution implemented
- [ ] Pre-commit hooks for secrets detection
- [ ] Rotate compromised credentials immediately
- [ ] Regular secrets auditing process

## References
- [The State of Secrets Sprawl 2025](https://www.gitguardian.com/state-of-secrets-sprawl-report-2025): "In 2024 GitGuardian scanned 69.6M public repositories of which at least 4.61% contained a secret."
- [How did Openai detect that my API key was pushed to GitHub?](https://www.reddit.com/r/OpenAI/comments/zotyq4/how_did_openai_detect_that_my_api_key_was_pushed/): Reddit user surprised because OpenAI contacted him seconds after pushing an API key to GitHub.

[^1]: [23 million secrets spilled on GitHub, developers naively assume no one will know](https://cybernews.com/security/developers-hardcoding-secrets-github-risk/)
[^2]: [Analysis of GitHub Repositories Surfaces Nearly 23M Secrets](https://devops.com/analysis-of-github-repositories-surfaces-nearly-23m-secrets/)
[^3]: [Over 12 million auth secrets and keys leaked on GitHub in 2023](https://www.bleepingcomputer.com/news/security/over-12-million-auth-secrets-and-keys-leaked-on-github-in-2023/)
[^4]: [The State of Secrets Sprawl 2024](https://securityboulevard.com/2024/03/the-state-of-secrets-sprawl-2024/)