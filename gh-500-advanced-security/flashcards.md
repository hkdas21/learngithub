---
layout: certification
title: "Flashcards"
cert_code: "GH-500"
cert_title: "GitHub Advanced Security"
cert_path: "/gh-500-advanced-security/"
cert_color: "#DA3633"
section: flashcards
---

# GitHub Advanced Security (GH-500) — Flashcards

Click on each term to reveal its definition.

---

<details>
<summary>GitHub Advanced Security (GHAS)</summary>

A suite of security features built into GitHub that helps teams find and fix vulnerabilities in code, secrets, and dependencies. GHAS includes code scanning, secret scanning, push protection, and dependency review. It is free for public repositories and requires a GitHub Enterprise plan plus a GHAS license for private/internal repositories.
</details>

---

<details>
<summary>Code Scanning</summary>

A GHAS feature that analyzes source code to find security vulnerabilities and coding errors. It runs via GitHub Actions workflows (typically using CodeQL) and displays results as alerts in the Security tab and as pull request annotations. It also supports third-party SARIF-compatible tools.
</details>

---

<details>
<summary>Secret Scanning</summary>

A GHAS feature that automatically searches a repository's entire Git history for known secret patterns such as API keys, tokens, and credentials. It supports over 200 partner patterns and allows organizations to define custom patterns using regular expressions. When a secret is detected, an alert is created and the partner provider may be notified.
</details>

---

<details>
<summary>Push Protection</summary>

A secret scanning feature that blocks pushes containing recognized secrets before they reach the repository. When triggered, the developer is informed of the detected secret and must either remove it or provide a bypass reason (false positive, used in tests, or will fix later). All bypasses are logged for admin review.
</details>

---

<details>
<summary>CodeQL</summary>

GitHub's semantic code analysis engine that treats code as data. It creates a relational database from a codebase and runs queries written in the QL language to find vulnerabilities. CodeQL supports C/C++, C#, Go, Java/Kotlin, JavaScript/TypeScript, Python, Ruby, and Swift. It is the default engine powering GitHub code scanning.
</details>

---

<details>
<summary>SARIF</summary>

**Static Analysis Results Interchange Format** — a JSON-based OASIS standard (version 2.1.0 supported by GitHub) that provides a common output format for static analysis tools. GitHub code scanning accepts SARIF files from any compatible tool, enabling integration with third-party analyzers beyond CodeQL.
</details>

---

<details>
<summary>Dependency Graph</summary>

A GitHub feature that automatically parses manifest and lock files to identify all direct and transitive dependencies of a repository. It is visible under the Insights tab and powers Dependabot alerts and the dependency review action. Supported ecosystems include npm, pip, Maven, RubyGems, NuGet, and more.
</details>

---

<details>
<summary>Dependabot Alerts</summary>

Notifications generated when a dependency in a repository has a known vulnerability listed in the GitHub Advisory Database. Each alert includes the affected dependency, vulnerable version range, severity level, and the patched version if available. Alerts appear under the Security tab.
</details>

---

<details>
<summary>Dependabot Security Updates</summary>

Automatic pull requests created by Dependabot to update a vulnerable dependency to the minimum patched version. These are triggered by Dependabot alerts and are enabled at the repository level. The PRs include release notes, changelogs, and compatibility information to help maintainers review the update.
</details>

---

<details>
<summary>Dependabot Version Updates</summary>

Proactive pull requests created by Dependabot to keep dependencies up to date regardless of known vulnerabilities. Configured via a `.github/dependabot.yml` file that specifies the package ecosystem, directory, update schedule (daily, weekly, or monthly), open PR limits, and other options like grouping and labeling.
</details>

---

<details>
<summary>Dependency Review</summary>

A GitHub Actions workflow step that runs on pull requests to compare dependency changes before and after the PR. It flags newly introduced dependencies with known vulnerabilities and can fail the check based on configurable severity thresholds. It also supports license compliance checks via allow-list and deny-list settings.
</details>

---

<details>
<summary>Security Advisory</summary>

A repository-level feature that allows maintainers to privately discuss, document, and remediate a vulnerability. Maintainers can request a CVE identifier from GitHub (a CVE Numbering Authority), create a private fork for developing a fix, and publish the advisory when ready. Published advisories can automatically trigger Dependabot alerts for downstream users.
</details>

---

<details>
<summary>Security Policy (SECURITY.md)</summary>

A Markdown file placed in the repository root or `.github/` directory that tells contributors how to responsibly report security vulnerabilities. GitHub displays a link to this file on the repository's Security tab. It should include the scope of coverage, reporting instructions, and expected response timelines.
</details>

---

<details>
<summary>Custom Secret Pattern</summary>

A user-defined regular expression pattern for secret scanning that extends detection beyond the built-in partner patterns. Custom patterns can be defined at the repository, organization, or enterprise level. Each pattern includes a name, a secret format regex, and optional before/after context patterns to reduce false positives.
</details>

---

<details>
<summary>Security Overview Dashboard</summary>

An organization-level dashboard that provides a consolidated view of code scanning, secret scanning, and Dependabot alerts across all repositories. It allows security teams to filter alerts by severity, tool, repository, and team. It also provides trend and coverage views for tracking remediation progress over time.
</details>
