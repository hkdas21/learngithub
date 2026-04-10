---
layout: certification
title: "Exam Overview"
cert_code: "GH-500"
cert_title: "GitHub Advanced Security"
cert_path: "/gh-500-advanced-security/"
cert_color: "#DA3633"
section: overview
---

# GitHub Advanced Security (GH-500) — Exam Overview

## About This Certification

The **GitHub Advanced Security** certification validates your skills in configuring and using GitHub Advanced Security (GHAS) features. This includes code scanning, secret scanning, dependency review, and security policies. Earning this certification demonstrates that you can effectively secure codebases and supply chains using the full suite of GHAS tools integrated into the GitHub platform.

## Exam Details

| Detail | Value |
|---|---|
| **Exam Code** | GH-500 |
| **Duration** | 120 minutes |
| **Number of Questions** | 75 |
| **Passing Score** | 70% |
| **Question Format** | Multiple choice / Multiple select |
| **Cost** | $99 USD |

## Exam Domains

| Domain | Weight |
|---|---|
| Describe the GHAS security features and functionality | 10% |
| Configure and use secret scanning | 20% |
| Configure and use code scanning | 20% |
| Use code scanning with CodeQL | 20% |
| Describe GitHub Advanced Security best practices, results, and how to take corrective measures | 10% |
| Configure and use dependency management | 20% |

## Preparation Tips

- **Get hands-on with GHAS features.** The exam is heavily practical. Enable secret scanning, code scanning, and Dependabot on a test repository and work through real alerts. There is no substitute for direct experience.
- **Practice writing and running CodeQL queries.** CodeQL carries a significant portion of the exam. Install the CodeQL CLI, explore the standard query suites, and write at least one simple custom query against a sample codebase.
- **Understand the full Dependabot lifecycle.** Know the difference between Dependabot alerts, security updates, and version updates. Practice configuring `dependabot.yml` and reviewing the pull requests it generates.
- **Explore the Security Overview dashboard.** Navigate the organization-level security overview, filter by severity and tool, and understand how to track remediation progress across multiple repositories.
- **Know the configuration files and formats.** Be comfortable with CodeQL workflow YAML, `dependabot.yml`, SARIF format basics, custom secret scanning patterns, and the `SECURITY.md` policy file.
- **Review the GitHub documentation.** The official GitHub Advanced Security docs are the primary source of truth. Pay special attention to feature availability across GitHub plans (Free, Team, Enterprise Cloud, Enterprise Server).
