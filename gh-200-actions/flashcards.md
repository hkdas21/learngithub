---
layout: certification
title: "Flashcards"
cert_code: "GH-200"
cert_title: "GitHub Actions"
cert_path: "/gh-200-actions/"
cert_color: "#F9826C"
section: flashcards
---

# GitHub Actions Certification (GH-200) -- Flashcards

Click on each term to reveal its definition and key details.

---

### 1. Workflow

<details>
<summary>What is a Workflow?</summary>

A **workflow** is an automated process defined in a YAML file inside the `.github/workflows/` directory of a repository. Each workflow consists of one or more jobs and is triggered by events, manual dispatch, or a schedule. A single repository can contain multiple workflows.

</details>

---

### 2. Job

<details>
<summary>What is a Job?</summary>

A **job** is a set of steps that execute on the same runner. Jobs within a workflow run in parallel by default. You can create dependencies between jobs using the `needs` keyword to enforce sequential execution. Each job runs in a fresh runner instance.

</details>

---

### 3. Step

<details>
<summary>What is a Step?</summary>

A **step** is an individual task within a job. Steps run sequentially in the order they are defined. A step can either run a shell command (using the `run` keyword) or invoke an action (using the `uses` keyword). Steps can have names, IDs, conditional logic, and environment variables.

</details>

---

### 4. Runner

<details>
<summary>What is a Runner?</summary>

A **runner** is a server that executes workflow jobs. GitHub provides **hosted runners** (Ubuntu, Windows, macOS) that offer a clean VM for every job. Organizations can also register **self-hosted runners** on their own infrastructure for custom hardware, software, or network requirements. Runners are specified with the `runs-on` key.

</details>

---

### 5. Event / Trigger

<details>
<summary>What is an Event (Trigger)?</summary>

An **event** is a specific activity that triggers a workflow. Common events include `push`, `pull_request`, `workflow_dispatch` (manual), `schedule` (cron-based), and `repository_dispatch` (API-based). Events are specified under the `on` key in a workflow file and can be filtered by branches, tags, paths, and activity types.

</details>

---

### 6. Action

<details>
<summary>What is an Action?</summary>

An **action** is a reusable unit of code that performs a specific task within a workflow step. Actions can be **JavaScript actions** (run with Node.js), **Docker container actions** (run in a container), or **composite actions** (combine multiple steps). Actions are referenced with the `uses` keyword and can be sourced from the GitHub Marketplace, other repositories, or the local repository.

</details>

---

### 7. Artifact

<details>
<summary>What is an Artifact?</summary>

An **artifact** is a file or collection of files produced during a workflow run that can be persisted and shared. Use `actions/upload-artifact` to save artifacts and `actions/download-artifact` to retrieve them in subsequent jobs. Artifacts are commonly used for build outputs, test reports, and log files. Default retention is 90 days.

</details>

---

### 8. Secret

<details>
<summary>What is a Secret?</summary>

A **secret** is an encrypted environment variable stored at the repository, environment, or organization level. Secrets are accessed via the `secrets` context (e.g., `${{ secrets.API_KEY }}`). Their values are automatically masked in workflow logs. Secrets are not exposed to workflows triggered from forked repositories. The `GITHUB_TOKEN` is a special automatically-generated secret scoped to the repository.

</details>

---

### 9. Context

<details>
<summary>What is a Context?</summary>

A **context** is a set of information available during a workflow run, accessed using `${{ context.property }}` syntax. Key contexts include `github` (event and repo info), `env` (environment variables), `secrets` (encrypted secrets), `steps` (step outputs and outcomes), `matrix` (current matrix values), `runner` (runner details), and `inputs` (workflow or action inputs).

</details>

---

### 10. Expression

<details>
<summary>What is an Expression?</summary>

An **expression** is a construct enclosed in `${{ }}` that is evaluated at runtime. Expressions can reference contexts, use comparison operators (`==`, `!=`, `<`, `>`), logical operators (`&&`, `||`, `!`), and call built-in functions such as `contains()`, `startsWith()`, `hashFiles()`, `toJSON()`, and `format()`. They are used in `if` conditionals, `env` values, and input parameters.

</details>

---

### 11. Matrix Strategy

<details>
<summary>What is a Matrix Strategy?</summary>

A **matrix strategy** allows a single job definition to run multiple times with different variable combinations. Defined under `strategy.matrix`, you specify arrays of values (e.g., OS versions, language versions) and GitHub Actions creates a job for every combination. Use `include` to add extra combinations, `exclude` to remove specific ones, `fail-fast` to control cancellation behavior, and `max-parallel` to limit concurrency.

</details>

---

### 12. Reusable Workflow

<details>
<summary>What is a Reusable Workflow?</summary>

A **reusable workflow** is a workflow that can be called from other workflows, enabling DRY (Don't Repeat Yourself) automation. It is defined with the `on: workflow_call` trigger and can accept `inputs` and `secrets`. The calling workflow references it at the job level using `uses: {owner}/{repo}/.github/workflows/{file}@{ref}`. Reusable workflows support up to four levels of nesting and can return outputs to the caller.

</details>

---

### 13. Composite Action

<details>
<summary>What is a Composite Action?</summary>

A **composite action** bundles multiple steps (shell commands and/or references to other actions) into a single reusable action. Defined with `runs.using: composite` in the `action.yml` file. Each `run` step must explicitly specify a `shell`. Composite actions support inputs and outputs, making them a lightweight alternative to JavaScript or Docker actions when you need to reuse a sequence of steps.

</details>

---

### 14. Self-Hosted Runner

<details>
<summary>What is a Self-Hosted Runner?</summary>

A **self-hosted runner** is a machine that you provision and manage, registered with a repository, organization, or enterprise to execute workflow jobs. Self-hosted runners are useful when you need custom hardware (GPUs, ARM processors), specific software, or network access to internal resources. They support Linux, Windows, and macOS. You are responsible for OS updates, security patches, and the runner application itself. They do not consume GitHub-billed minutes.

</details>

---

### 15. Environment Protection Rule

<details>
<summary>What is an Environment Protection Rule?</summary>

An **environment protection rule** is a safeguard applied to a deployment environment that gates job execution. There are three types: **required reviewers** (designated approvers must authorize the deployment), **wait timer** (a configurable delay in minutes before the job proceeds), and **deployment branches** (restricts which branches can deploy to the environment). Protection rules create manual approval gates and enforce governance in CI/CD pipelines.

</details>
