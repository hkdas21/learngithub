---
layout: certification
title: "Practice Quiz"
cert_code: "GH-200"
cert_title: "GitHub Actions"
cert_path: "/gh-200-actions/"
cert_color: "#F9826C"
section: quiz
---

# GitHub Actions Certification (GH-200) -- Practice Quiz

Test your knowledge with these 10 practice questions. Click on each question to reveal the answer and explanation.

---

### Question 1 -- Workflow Triggers

Which workflow trigger allows you to run a workflow on a recurring schedule using cron syntax?

- A) `workflow_dispatch`
- B) `repository_dispatch`
- C) `schedule`
- D) `push`

<details>
<summary>Show Answer</summary>

**Correct Answer: C) `schedule`**

The `schedule` trigger uses POSIX cron syntax to run workflows at defined intervals. For example, `cron: '0 6 * * 1'` runs every Monday at 06:00 UTC. `workflow_dispatch` is for manual triggers, `repository_dispatch` is for external API-triggered events, and `push` fires when commits are pushed.

</details>

---

### Question 2 -- Secrets

What happens when you attempt to print a secret's value to the workflow logs?

- A) The secret is displayed in plain text.
- B) The workflow fails with a security error.
- C) The secret value is automatically masked with `***`.
- D) The step is skipped entirely.

<details>
<summary>Show Answer</summary>

**Correct Answer: C) The secret value is automatically masked with `***`.**

GitHub Actions automatically redacts secret values from log output, replacing them with `***`. This prevents accidental exposure. However, you should still be careful with structured output -- if a secret is transformed (e.g., base64-encoded), the transformed value may not be masked.

</details>

---

### Question 3 -- Matrix Strategy

Given the following matrix configuration, how many jobs will run?

```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest]
    node: [18, 20, 22]
    exclude:
      - os: windows-latest
        node: 18
```

- A) 3
- B) 5
- C) 6
- D) 9

<details>
<summary>Show Answer</summary>

**Correct Answer: B) 5**

Without exclusions, the matrix produces 2 OS x 3 Node versions = 6 combinations. The `exclude` block removes one combination (Windows + Node 18), leaving 5 jobs: Ubuntu/18, Ubuntu/20, Ubuntu/22, Windows/20, and Windows/22.

</details>

---

### Question 4 -- Runner Types

Which of the following is true about GitHub-hosted runners?

- A) They persist state between workflow runs.
- B) They are only available on Linux.
- C) They provide a clean virtual machine for every job.
- D) They do not have any pre-installed software.

<details>
<summary>Show Answer</summary>

**Correct Answer: C) They provide a clean virtual machine for every job.**

GitHub-hosted runners spin up a fresh VM for each job and are destroyed afterward, ensuring a clean environment. They are available on Linux, Windows, and macOS (not just Linux). They come with a wide selection of pre-installed software and tools.

</details>

---

### Question 5 -- Artifacts

What is the default retention period for artifacts uploaded with `actions/upload-artifact`?

- A) 7 days
- B) 30 days
- C) 90 days
- D) 365 days

<details>
<summary>Show Answer</summary>

**Correct Answer: C) 90 days**

By default, artifacts and log files are retained for 90 days. This can be customized using the `retention-days` input on the `actions/upload-artifact` action or configured at the repository or organization level in settings. The maximum retention is 90 days for public repos and varies by plan for private repos.

</details>

---

### Question 6 -- Reusable Workflows

How do you invoke a reusable workflow from a calling workflow?

- A) Using the `run` keyword with the workflow path.
- B) Using the `uses` keyword at the job level with the workflow file reference.
- C) Using the `call` keyword followed by the workflow name.
- D) Using the `imports` keyword in the workflow header.

<details>
<summary>Show Answer</summary>

**Correct Answer: B) Using the `uses` keyword at the job level with the workflow file reference.**

A reusable workflow is invoked at the **job level** using the `uses` keyword, for example: `uses: octo-org/shared-workflows/.github/workflows/ci.yml@main`. The reusable workflow must define `on: workflow_call` as its trigger. The `run` keyword is for shell commands, and `call` and `imports` are not valid workflow keywords.

</details>

---

### Question 7 -- Environment Protection Rules

Which of the following are valid environment protection rules in GitHub Actions? (Select all that apply.)

- A) Required reviewers
- B) Wait timer
- C) Deployment branches
- D) Mandatory labels

<details>
<summary>Show Answer</summary>

**Correct Answers: A) Required reviewers, B) Wait timer, C) Deployment branches**

GitHub environments support three protection rules: **required reviewers** (one or more people must approve), **wait timer** (a delay in minutes before the job proceeds), and **deployment branches** (restricts which branches can deploy to the environment). "Mandatory labels" is not a valid environment protection rule.

</details>

---

### Question 8 -- Action Types

Which type of custom action can only run on Linux runners?

- A) JavaScript action
- B) Composite action
- C) Docker container action
- D) TypeScript action

<details>
<summary>Show Answer</summary>

**Correct Answer: C) Docker container action**

Docker container actions are limited to Linux runners because they rely on Docker, which is only supported on Linux-based GitHub-hosted runners. JavaScript actions and composite actions can run on Linux, Windows, and macOS runners. "TypeScript action" is not a distinct action type -- TypeScript is compiled to JavaScript.

</details>

---

### Question 9 -- Caching

Which function is commonly used to generate a dynamic cache key based on dependency lock files?

- A) `toJSON()`
- B) `hashFiles()`
- C) `format()`
- D) `contains()`

<details>
<summary>Show Answer</summary>

**Correct Answer: B) `hashFiles()`**

The `hashFiles()` function generates a SHA-256 hash of one or more files, and is commonly used to create cache keys based on lock files. For example: `key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}`. This ensures the cache is invalidated whenever dependencies change.

</details>

---

### Question 10 -- GITHUB_TOKEN Permissions

What is the default permission scope of the `GITHUB_TOKEN` in a workflow?

- A) No permissions at all.
- B) Read and write access to all repository resources.
- C) Depends on the repository or organization setting (restrictive or permissive).
- D) Read-only access to the repository contents only.

<details>
<summary>Show Answer</summary>

**Correct Answer: C) Depends on the repository or organization setting (restrictive or permissive).**

The default `GITHUB_TOKEN` permissions depend on the repository or organization configuration. Organizations and repositories can choose between a **permissive** default (read/write for most scopes) or a **restrictive** default (read-only for contents and metadata). GitHub recommends the restrictive setting. Regardless of the default, you can explicitly set permissions in your workflow using the `permissions` key at the workflow or job level.

</details>
