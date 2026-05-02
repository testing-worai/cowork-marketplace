# Security Policy

Work On Referrals, Inc. takes the security of `wor-training` and its backend MCP server seriously. We welcome reports from users, researchers, and Anthropic.

## Reporting a Vulnerability

Email reports to: **[operations@workonreferrals.com](mailto:operations@workonreferrals.com)**

Please include, where possible:

- A description of the vulnerability and its impact
- Steps to reproduce, or a proof-of-concept
- The affected component (plugin source, remote MCP endpoint, billing flow, etc.)
- Your name and contact information for follow-up

We aim to acknowledge new reports within **two business days** and to investigate with reasonable care. We may contact you for additional details during triage.

## Scope

In scope:

- The plugin source in this repository
- The remote MCP server at `https://yue9grn54i.us-east-1.awsapprunner.com/mcp`
- Authentication and license-validation flows
- The Stripe webhook handler (signature verification, license issuance, email delivery)

Out of scope (please report directly to the upstream):

- Stripe — report to [https://www.stripe.com/security](https://www.stripe.com/security)
- Resend — report to [https://resend.com/security](https://resend.com/security)
- AWS — report via [https://aws.amazon.com/security/vulnerability-reporting/](https://aws.amazon.com/security/vulnerability-reporting/)
- Issues in Claude Cowork itself — report to Anthropic

## Disclosure

We follow coordinated disclosure. Once a fix is in place we will work with you on a public disclosure timeline that gives users a reasonable window to update.

## Out-of-Band Reports

Anthropic, as the directory operator, may report vulnerabilities to the same address per §3.H of the Anthropic Software Directory Terms.
