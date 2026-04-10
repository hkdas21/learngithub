---
layout: certification
title: "Study Notes"
cert_code: "GH-500"
cert_title: "GitHub Advanced Security"
cert_path: "/gh-500-advanced-security/"
cert_color: "#DA3633"
section: study-notes
---

# GitHub Advanced Security (GH-500) — Study Notes

---

## Module 1: GHAS Overview

### What Is GitHub Advanced Security?

GitHub Advanced Security (GHAS) is a suite of security features built into GitHub that helps teams find and fix vulnerabilities in their code, secrets, and dependencies. GHAS extends the native security capabilities of GitHub with advanced tooling designed for enterprise-scale development.

### Availability by Plan

| Feature | GitHub Free (Public) | GitHub Free (Private) | GitHub Team | GitHub Enterprise Cloud | GitHub Enterprise Server |
|---|---|---|---|---|---|
| Dependency graph | Yes | Yes | Yes | Yes | Yes |
| Dependabot alerts | Yes | Yes | Yes | Yes | Yes |
| Dependabot security updates | Yes | Yes | Yes | Yes | Yes |
| Secret scanning (partner patterns) | Yes | No | No | Yes (with GHAS license) | Yes (with GHAS license) |
| Secret scanning (user-defined patterns) | No | No | No | Yes (with GHAS license) | Yes (with GHAS license) |
| Code scanning | Yes | No | No | Yes (with GHAS license) | Yes (with GHAS license) |
| Push protection | Yes | No | No | Yes (with GHAS license) | Yes (with GHAS license) |

- GHAS is **free for public repositories** on GitHub.com.
- For private and internal repositories, GHAS requires a **GitHub Enterprise** plan plus a **GHAS license**.

### Feature Matrix

- **Code Scanning** — Finds potential security vulnerabilities and coding errors in your code.
- **Secret Scanning** — Detects secrets (tokens, keys, passwords) that have been committed to a repository.
- **Push Protection** — Prevents secrets from being pushed in the first place.
- **Dependency Review** — Shows the impact of dependency changes in pull requests before they are merged.

### Security Overview Dashboard

The **Security Overview** is an organization-level dashboard that provides a consolidated view of security alerts across all repositories. It allows security teams to:

- View code scanning, secret scanning, and Dependabot alerts in one place.
- Filter by alert severity, tool, and repository.
- Track remediation trends over time.
- Identify the repositories with the highest risk.

---

## Module 2: Secret Scanning

### How Secret Scanning Works

Secret scanning automatically searches your repository's entire Git history for known secret patterns (API keys, tokens, credentials). When a match is found, GitHub generates an alert and optionally notifies the secret's provider.

### Supported Patterns

GitHub supports **200+ secret patterns** from partner providers including:

- AWS access keys
- Azure storage account keys
- Google Cloud API keys
- GitHub personal access tokens
- Slack tokens, Stripe keys, Twilio keys, and many more

### Custom Patterns

Organizations can define **custom secret patterns** using regular expressions. Custom patterns can be defined at:

- **Repository level** — applies to a single repo.
- **Organization level** — applies to all repos in the org.
- **Enterprise level** — applies across all organizations.

Each custom pattern includes:
- A **pattern name** and description.
- A **secret format** (regex).
- Optional **before-secret** and **after-secret** context patterns to reduce false positives.

### Push Protection

Push protection **blocks pushes** that contain recognized secrets before they reach the repository. When a developer attempts to push a commit containing a secret:

1. The push is blocked with an error message.
2. The developer is told which secret was detected and on which line.
3. The developer can choose to **bypass** the protection (if allowed) by providing a reason: false positive, used in tests, or will fix later.
4. Bypasses are logged and visible to organization admins.

### Partner Program

When a secret from a **partner provider** is detected, GitHub notifies the provider directly so they can revoke or rotate the credential. This happens automatically and provides an extra layer of protection.

### Alert Management

- Alerts can be **open**, **resolved**, or **dismissed** (with a reason: false positive, used in tests, revoked, or won't fix).
- Alerts include the commit SHA, file path, and line number where the secret was detected.
- Organization owners can view all secret scanning alerts from the Security Overview.

---

## Module 3: Code Scanning

### Overview

Code scanning analyzes your source code to find security vulnerabilities and coding errors. Results appear as alerts in the repository's **Security** tab and as annotations in pull requests.

### Setting Up Code Scanning with Actions

The most common way to enable code scanning is through a **GitHub Actions workflow**:

1. Navigate to the repository's **Security** tab.
2. Click **Set up code scanning**.
3. Choose the **CodeQL Analysis** starter workflow.
4. Commit the workflow file (`.github/workflows/codeql.yml`) to the repository.

The default workflow:
- Runs on `push` to the default branch and on `pull_request` events.
- Runs on a schedule (e.g., weekly) to catch vulnerabilities in unchanged code with updated rules.
- Auto-detects the languages in the repository.

### Third-Party Tools

Code scanning is not limited to CodeQL. You can integrate any **SARIF-compatible** static analysis tool:

- Upload results via the `github/codeql-action/upload-sarif` action.
- Or use the REST API to upload SARIF files directly.

Popular third-party tools: **ESLint**, **Semgrep**, **SonarQube**, **Checkmarx**, **Snyk Code**.

### SARIF Format

**SARIF (Static Analysis Results Interchange Format)** is a JSON-based standard for static analysis output. Key elements:

- **`runs`** — Each run represents one execution of an analysis tool.
- **`results`** — Individual findings (alerts).
- **`rules`** — The rules/queries that produced the results.
- **`locations`** — File paths and line numbers where issues were found.

GitHub supports SARIF version **2.1.0**.

### Alert Triage and Dismissal

Each code scanning alert can be:

- **Open** — Needs attention.
- **Fixed** — The code was changed and the alert no longer appears.
- **Dismissed** — Manually dismissed with a reason:
  - **False positive** — The finding is incorrect.
  - **Won't fix** — The finding is accepted as a known risk.
  - **Used in tests** — The code is only used in test files.

Alerts can be filtered by **severity** (critical, high, medium, low), **tool**, **rule**, and **branch**.

---

## Module 4: CodeQL

### What Is CodeQL?

**CodeQL** is GitHub's semantic code analysis engine. It treats code as data by creating a **database** from the codebase, then runs **queries** against that database to find vulnerabilities. It supports: **C/C++, C#, Go, Java/Kotlin, JavaScript/TypeScript, Python, Ruby, and Swift**.

### CodeQL CLI

The **CodeQL CLI** is a standalone command-line tool for:

- Creating CodeQL databases from source code (`codeql database create`).
- Running queries against databases (`codeql database analyze`).
- Generating SARIF output for upload to GitHub.
- Testing and developing custom queries locally.

### Query Suites

CodeQL ships with pre-built **query suites**:

| Suite | Description |
|---|---|
| `code-scanning` | The default suite used by GitHub code scanning. Balanced for precision and recall. |
| `security-extended` | Includes additional security queries with slightly lower precision. |
| `security-and-quality` | Includes security queries plus code quality queries. |

You select the suite in the CodeQL workflow YAML using the `queries` key or the `query-filters` key.

### Custom Queries

Custom CodeQL queries are written in the **QL language** and follow this structure:

```ql
/**
 * @name Description of the query
 * @description Longer description
 * @kind problem
 * @problem.severity warning
 * @id custom/my-query
 */

import javascript

from CallExpr call
where call.getCalleeName() = "eval"
select call, "Avoid using eval()."
```

Key concepts:
- **`@kind`** — Defines the query type: `problem` (single location) or `path-problem` (data-flow path).
- **`import`** — Imports the language-specific CodeQL library.
- **`from`**, **`where`**, **`select`** — The query's logic (similar to SQL).

### CodeQL Packs

**CodeQL packs** are the distribution mechanism for CodeQL queries and libraries:

- **Query packs** — Contain queries that can be run directly.
- **Library packs** — Contain reusable QL libraries that query packs depend on.
- Published to and installed from the **GitHub Container Registry (GHCR)**.
- Defined by a `qlpack.yml` file.

### Analysis Configuration

Key configuration options in the CodeQL workflow:

- **`languages`** — Which languages to analyze.
- **`queries`** — Which query suites or custom queries to run.
- **`config-file`** — Path to a separate CodeQL configuration file.
- **`paths` / `paths-ignore`** — Include or exclude specific directories.
- **`build-mode`** — `autobuild` (default) or `manual` (for compiled languages needing a custom build).

---

## Module 5: Security Best Practices

### Security Policies

A **security policy** tells contributors how to responsibly report vulnerabilities in your project. It should include:

- The scope of the policy (which versions/branches are covered).
- How to report a vulnerability (email, private advisory, etc.).
- Expected response timeline.

### SECURITY.md

The `SECURITY.md` file lives in the repository root (or `.github/` directory). GitHub displays a link to it on the repository's **Security** tab. It is the standard location for your security policy.

### Security Advisories

**Repository security advisories** allow maintainers to:

1. **Privately discuss** a vulnerability with collaborators.
2. **Request a CVE** identifier from GitHub (GitHub is a CVE Numbering Authority).
3. **Create a private fork** to develop a fix without public disclosure.
4. **Publish the advisory** when the fix is ready, which can automatically trigger Dependabot alerts for affected downstream users.

### Coordinated Disclosure

Best practices for coordinated vulnerability disclosure:

- Use **private vulnerability reporting** (if enabled) to allow external researchers to report issues confidentially.
- Triage reports promptly and communicate a timeline for fixes.
- Publish the advisory and fix simultaneously.
- Credit the reporter in the advisory.

### Corrective Measures Workflow

When a security alert is found, the corrective workflow is:

1. **Triage** — Verify the finding is a true positive and assess severity.
2. **Prioritize** — Rank the issue based on severity, exploitability, and exposure.
3. **Remediate** — Fix the code, rotate the secret, or update the dependency.
4. **Verify** — Confirm the fix resolves the alert (re-scan).
5. **Close** — Dismiss or mark as resolved.
6. **Document** — Record the incident and update policies if needed.

---

## Module 6: Dependency Management

### Dependency Graph

The **dependency graph** is a summary of all the dependencies (and dependents) of a repository. It:

- Automatically parses manifest files (`package.json`, `pom.xml`, `Gemfile.lock`, `requirements.txt`, etc.).
- Shows direct and transitive dependencies.
- Is available under the repository's **Insights** tab.
- Powers Dependabot alerts and the dependency review action.

### Dependabot Alerts

**Dependabot alerts** notify repository maintainers when a dependency has a known vulnerability listed in the **GitHub Advisory Database**. Each alert includes:

- The affected dependency and vulnerable version range.
- The severity (critical, high, medium, low).
- A link to the advisory with remediation guidance.
- The patched version (if available).

### Dependabot Security Updates

**Dependabot security updates** automatically create **pull requests** to update vulnerable dependencies to the minimum patched version. Key points:

- Triggered by Dependabot alerts.
- Enabled at the repository level under **Settings > Code security and analysis**.
- PRs include release notes, changelog entries, and commit details.
- Only updates to the nearest safe version (minimal change).

### Dependabot Version Updates

**Dependabot version updates** proactively keep dependencies up to date, regardless of known vulnerabilities. Configured via `.github/dependabot.yml`:

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "monday"
    open-pull-requests-limit: 10
    reviewers:
      - "octocat"
    labels:
      - "dependencies"
```

Key configuration options:
- **`package-ecosystem`** — The package manager (npm, pip, maven, docker, github-actions, etc.).
- **`directory`** — Where the manifest file lives.
- **`schedule.interval`** — `daily`, `weekly`, or `monthly`.
- **`open-pull-requests-limit`** — Maximum number of open PRs (default: 5).
- **`allow` / `ignore`** — Filter which dependencies to update.
- **`groups`** — Group related updates into a single PR.

### Dependency Review Action

The **dependency review action** runs in pull requests and:

- Compares the dependencies before and after the PR.
- Flags newly introduced vulnerabilities.
- Can be configured to **block the PR** (fail the check) if vulnerable dependencies are added.
- Supports filtering by severity threshold and license types.

Usage in a workflow:

```yaml
- name: Dependency Review
  uses: actions/dependency-review-action@v4
  with:
    fail-on-severity: moderate
    deny-licenses: GPL-3.0
```

### License Compliance

The dependency review action also supports **license compliance** checks:

- **`allow-licenses`** — Only allow dependencies with specified licenses.
- **`deny-licenses`** — Block dependencies with specified licenses.
- Helps organizations enforce license policies automatically in the CI/CD pipeline.
