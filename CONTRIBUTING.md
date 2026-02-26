# Contributing to ClawSecure

Thank you for your interest in making the OpenClaw ecosystem safer. ClawSecure welcomes contributions from security researchers, OpenClaw developers, and community members.

## How to Contribute

### Report a Security Issue in an OpenClaw Skill

If you've found a vulnerability, suspicious behavior, or malicious code in an OpenClaw skill:

1. **Check the registry first** — Search the [Verified Agent Registry](https://www.clawsecure.ai/registry) to see if the skill has already been audited
2. **Submit a scan** — Use the [OpenClaw security scanner](https://www.clawsecure.ai/#scan) to run a free 3-Layer Audit on the skill
3. **File an issue** — If you've found something the scanner didn't catch, open a [Suspicious Skill Report](.github/ISSUE_TEMPLATE/skill_report.md) issue in this repository with details

Please include the skill URL, a description of the suspicious behavior, and any reproduction steps.

### Submit a Skill for Scanning

Any publicly available OpenClaw skill can be scanned for free:

- **Via URL** — Paste any ClawHub or GitHub skill URL into the scanner at [clawsecure.ai](https://www.clawsecure.ai/#scan)
- **Via file upload** — Upload a skill zip file directly through the scanner interface

Results are delivered in seconds as a full Security Audit Report covering all 10 OWASP ASI categories.

### Request a Feature

Have an idea for improving ClawSecure? Open a [Feature Request](.github/ISSUE_TEMPLATE/feature_request.md) issue. We're especially interested in:

- New threat patterns for OpenClaw-specific attack vectors
- Security Clearance API integration ideas
- Improvements to the Verified Agent Registry
- OWASP ASI coverage enhancements

### Report a Platform Bug

Found a bug in the ClawSecure platform itself? Open a [Bug Report](.github/ISSUE_TEMPLATE/bug_report.md) issue with steps to reproduce.

## Security Vulnerability Disclosure

If you've found a security vulnerability in **ClawSecure itself** (not in an OpenClaw skill), please see [SECURITY.md](SECURITY.md) for our responsible disclosure process. Do not open a public issue for security vulnerabilities.

## Code of Conduct

We are committed to providing a welcoming and respectful environment for everyone contributing to OpenClaw security. Contributors are expected to:

- Be respectful and constructive in all interactions
- Focus on the technical merits of security findings
- Avoid disclosing active vulnerabilities publicly before responsible disclosure
- Credit original researchers when referencing prior work

## Questions?

Visit [clawsecure.ai](https://www.clawsecure.ai), email us at contact@clawsecure.ai, or reach out on X/Twitter at [@ClawSecure](https://x.com/ClawSecure).
