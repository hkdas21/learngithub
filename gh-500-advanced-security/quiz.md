---
layout: certification
title: "Practice Quiz"
cert_code: "GH-500"
cert_title: "GitHub Advanced Security"
cert_path: "/gh-500-advanced-security/"
cert_color: "#DA3633"
section: quiz
---

# GitHub Advanced Security (GH-500) — Practice Quiz

Test your knowledge of GitHub Advanced Security concepts. Click on each question to reveal the answer.

---

**Question 1: GHAS Availability**

On which repository types is GitHub Advanced Security available without an additional license?

A. All private repositories on GitHub Team plans
B. All public repositories on GitHub.com
C. Only repositories on GitHub Enterprise Cloud
D. Only repositories on GitHub Enterprise Server

<details>
<summary>Show Answer</summary>

**B. All public repositories on GitHub.com**

GitHub Advanced Security features (code scanning, secret scanning, push protection) are available for free on all public repositories on GitHub.com. For private and internal repositories, a GitHub Enterprise plan plus a GHAS license is required.
</details>

---

**Question 2: Secret Scanning Patterns**

What types of patterns does GitHub secret scanning detect by default?

A. Only patterns defined by the repository administrator
B. Only GitHub personal access tokens
C. Over 200 known secret patterns from partner providers
D. Any string that looks like a password

<details>
<summary>Show Answer</summary>

**C. Over 200 known secret patterns from partner providers**

GitHub secret scanning supports over 200 known secret patterns from partner providers including AWS, Azure, Google Cloud, Slack, Stripe, and many others. Organizations can also define custom patterns using regular expressions.
</details>

---

**Question 3: Push Protection**

What happens when a developer tries to push a commit that contains a recognized secret and push protection is enabled?

A. The push succeeds but an email is sent to the organization admin
B. The push is blocked, and the developer must remove the secret or provide a bypass reason
C. The secret is automatically redacted from the commit
D. The push succeeds but the repository is locked until the secret is removed

<details>
<summary>Show Answer</summary>

**B. The push is blocked, and the developer must remove the secret or provide a bypass reason**

Push protection blocks the push and informs the developer which secret was detected and on which line. The developer can either remove the secret and push again, or bypass the protection by providing a reason (false positive, used in tests, or will fix later). All bypasses are logged for organization admins to review.
</details>

---

**Question 4: CodeQL Query Language**

What is the basic structure of a CodeQL query?

A. `SELECT ... FROM ... WHERE ...` using standard SQL syntax
B. `from ... where ... select ...` using QL syntax
C. `MATCH ... RETURN ...` using Cypher graph query syntax
D. `find ... filter ... output ...` using a custom DSL

<details>
<summary>Show Answer</summary>

**B. `from ... where ... select ...` using QL syntax**

CodeQL queries use the QL language with a structure that resembles SQL but is specifically designed for code analysis. A basic query defines variables in the `from` clause, constrains them in the `where` clause, and specifies what to output in the `select` clause.
</details>

---

**Question 5: SARIF Format**

What is SARIF and how is it used with GitHub code scanning?

A. A proprietary binary format used only by CodeQL
B. A YAML-based configuration format for defining scan rules
C. A JSON-based standard for static analysis results that GitHub uses to display code scanning alerts
D. A log format used by GitHub Actions to record workflow runs

<details>
<summary>Show Answer</summary>

**C. A JSON-based standard for static analysis results that GitHub uses to display code scanning alerts**

SARIF (Static Analysis Results Interchange Format) is a JSON-based OASIS standard (version 2.1.0 supported by GitHub) that defines a common format for static analysis tool output. GitHub accepts SARIF files from any compatible tool, not just CodeQL, making code scanning extensible to third-party analyzers.
</details>

---

**Question 6: Code Scanning Alerts**

Which of the following is NOT a valid reason for dismissing a code scanning alert?

A. False positive
B. Won't fix
C. Used in tests
D. Duplicate finding

<details>
<summary>Show Answer</summary>

**D. Duplicate finding**

The valid dismissal reasons for code scanning alerts are: **False positive** (the finding is incorrect), **Won't fix** (the finding is accepted as a known risk), and **Used in tests** (the code is only used in test files). "Duplicate finding" is not a built-in dismissal reason in GitHub code scanning.
</details>

---

**Question 7: Dependabot Configuration**

In a `dependabot.yml` file, what does the `open-pull-requests-limit` setting control?

A. The maximum number of repositories Dependabot can create PRs for
B. The maximum number of open Dependabot pull requests allowed at one time per ecosystem and directory
C. The total number of PRs Dependabot can create per month
D. The maximum number of dependencies that can be updated in a single PR

<details>
<summary>Show Answer</summary>

**B. The maximum number of open Dependabot pull requests allowed at one time per ecosystem and directory**

The `open-pull-requests-limit` setting (default: 5) controls how many open Dependabot version update pull requests can exist simultaneously for each package ecosystem and directory combination. Once the limit is reached, Dependabot will not create new PRs until existing ones are merged or closed.
</details>

---

**Question 8: Dependency Review**

When does the dependency review action run, and what does it check?

A. It runs on every push and checks all existing dependencies for vulnerabilities
B. It runs on pull requests and checks whether newly introduced dependencies have known vulnerabilities
C. It runs on a weekly schedule and generates a full dependency audit report
D. It runs on merge and blocks the merge if any dependency is outdated

<details>
<summary>Show Answer</summary>

**B. It runs on pull requests and checks whether newly introduced dependencies have known vulnerabilities**

The dependency review action is designed to run on pull request events. It compares the dependency changes in the PR (before and after) and flags any newly introduced dependencies that have known vulnerabilities. It can be configured to fail the check based on severity thresholds and license restrictions.
</details>

---

**Question 9: Security Advisories**

Which of the following capabilities does GitHub's repository security advisory feature provide? (Select all that apply.)

A. Private discussion space for vulnerability details
B. Ability to request a CVE identifier directly from GitHub
C. Automatic patching of the vulnerable code
D. Private fork for developing a fix before public disclosure

<details>
<summary>Show Answer</summary>

**A, B, and D.**

Repository security advisories allow maintainers to privately discuss a vulnerability (A), request a CVE identifier from GitHub since GitHub is a CVE Numbering Authority (B), and create a private fork to develop a fix before public disclosure (D). GitHub does **not** automatically patch vulnerable code (C) — maintainers must develop the fix themselves.
</details>

---

**Question 10: Security Overview**

What is the primary purpose of the Security Overview dashboard at the organization level?

A. To configure security settings for all repositories at once
B. To provide a consolidated view of security alerts across all repositories in the organization
C. To automatically fix all open security alerts
D. To manage user access and permissions for security features

<details>
<summary>Show Answer</summary>

**B. To provide a consolidated view of security alerts across all repositories in the organization**

The Security Overview dashboard gives organization admins and security teams a centralized view of code scanning, secret scanning, and Dependabot alerts across all repositories. It supports filtering by severity, tool, repository, and team, and allows tracking remediation trends over time. It does not configure settings, fix alerts, or manage permissions.
</details>
