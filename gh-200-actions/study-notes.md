---
layout: certification
title: "Study Notes"
cert_code: "GH-200"
cert_title: "GitHub Actions"
cert_path: "/gh-200-actions/"
cert_color: "#F9826C"
section: study-notes
---

# GitHub Actions Certification (GH-200) -- Study Notes

---

## Module 1: Workflow Fundamentals

### YAML Syntax

- Workflows are defined in YAML files stored in the `.github/workflows/` directory.
- Key YAML concepts: key-value pairs, nested mappings, sequences (lists), multi-line strings (`|` for literal blocks, `>` for folded blocks).
- Indentation matters -- YAML uses spaces, never tabs.

### Workflow Files

- A repository can contain multiple workflow files.
- Each file defines one workflow with a `name`, `on` (trigger), and `jobs` section.
- Workflow files must have a `.yml` or `.yaml` extension.

### Events and Triggers

- **Push events:** `push` -- triggers when commits are pushed to a branch or tag.
- **Pull request events:** `pull_request` -- triggers on PR open, synchronize, reopen, and more.
- **Manual triggers:** `workflow_dispatch` -- allows manual runs with optional inputs.
- **Scheduled triggers:** `schedule` -- uses cron syntax (e.g., `cron: '0 6 * * 1'`).
- **Repository dispatch:** `repository_dispatch` -- triggers from external API calls.
- **Event filtering:** Use `branches`, `tags`, `paths`, and their `-ignore` variants to narrow trigger scope.

### Jobs

- A workflow contains one or more jobs that run in parallel by default.
- Use `needs` to define dependencies and create sequential execution.
- Each job runs on a fresh runner instance.
- Jobs are defined under the `jobs` key with a unique identifier.

### Steps

- Steps are the individual tasks within a job, executed sequentially.
- A step can run a shell command (`run`) or use an action (`uses`).
- Steps can have a `name`, `id`, `if` condition, and `env` variables.
- Data can be passed between steps using outputs and the `steps` context.

### Runner Types

- **GitHub-hosted runners:** Pre-configured VMs managed by GitHub (Ubuntu, Windows, macOS).
- **Self-hosted runners:** Machines you manage, registered with your repository or organization.
- Specified with the `runs-on` key (e.g., `runs-on: ubuntu-latest`).
- GitHub-hosted runners provide a clean environment for every job.

---

## Module 2: Authoring Workflows

### Conditional Execution

- Use the `if` keyword on jobs or steps to control execution.
- Status-check functions: `success()`, `failure()`, `always()`, `cancelled()`.
- Example: `if: failure()` runs a step only when a previous step has failed.
- Combine conditions with `&&`, `||`, and `!` operators.

### Matrix Strategies

- The `strategy.matrix` key lets you run a job across multiple configurations.
- Define variables (e.g., `os: [ubuntu-latest, windows-latest]`, `node: [16, 18, 20]`) and the job runs for every combination.
- Use `include` to add specific combinations and `exclude` to remove them.
- `fail-fast` (default `true`) cancels remaining matrix jobs when one fails.
- `max-parallel` limits the number of concurrent matrix jobs.

### Environment Variables

- Set at the workflow, job, or step level using the `env` key.
- Access with `${{ env.MY_VAR }}` in expressions or `$MY_VAR` in shell commands.
- Default environment variables: `GITHUB_SHA`, `GITHUB_REF`, `GITHUB_REPOSITORY`, `GITHUB_ACTOR`, etc.

### Secrets

- Stored in repository, environment, or organization settings.
- Referenced via `${{ secrets.MY_SECRET }}` -- values are masked in logs.
- `GITHUB_TOKEN` is automatically available and scoped to the repository.
- Secrets are not passed to workflows triggered by forks (for security).

### Contexts

- Contexts provide information about the workflow run, environment, and runner.
- Key contexts: `github`, `env`, `vars`, `secrets`, `steps`, `job`, `jobs`, `runner`, `inputs`, `matrix`.
- Accessed with `${{ context.property }}` syntax.
- The `github` context includes event payload data, repository info, actor, and more.

### Expressions

- Enclosed in `${{ }}` and evaluated at runtime.
- Support literals, operators, functions, and context references.
- Built-in functions: `contains()`, `startsWith()`, `endsWith()`, `format()`, `join()`, `toJSON()`, `fromJSON()`, `hashFiles()`.
- Comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`.

---

## Module 3: Consuming Workflows

### Reusable Workflows

- Defined with `on: workflow_call` and invoked from another workflow using `uses`.
- Can accept `inputs` and `secrets` from the calling workflow.
- Referenced as `{owner}/{repo}/.github/workflows/{filename}@{ref}`.
- Support up to four levels of nesting.
- Outputs from reusable workflows can be consumed by the caller.

### Starter Workflows

- Organization-level template workflows stored in a `.github` repository.
- Appear in the "Actions" tab when creating new workflows.
- Consist of a workflow YAML file and an optional `properties.json` metadata file.
- Help standardize CI/CD practices across an organization.

### Marketplace Actions

- The GitHub Marketplace hosts thousands of community and verified actions.
- Actions are referenced by `{owner}/{repo}@{ref}` (e.g., `actions/checkout@v4`).
- Always review an action's source code and permissions before using it.
- Verified creators have a blue badge in the Marketplace.

### Versioning Actions

- Pin actions to a specific version using tags (`@v4`), SHA (`@a1b2c3d...`), or branches (`@main`).
- **SHA pinning** is the most secure approach -- it is immutable.
- **Tag pinning** (e.g., `@v4`) is convenient but can be moved by the action author.
- Dependabot can automatically update action versions in your workflows.

---

## Module 4: Custom Actions

### JavaScript Actions

- Run directly on the runner using Node.js (no container overhead).
- Use the `@actions/core` and `@actions/github` toolkit packages.
- Fast startup; work on all runner operating systems (Linux, Windows, macOS).
- Entry point specified with `runs.using: node20` and `runs.main` in `action.yml`.

### Docker Container Actions

- Package the action in a Docker container for full control over the environment.
- Only run on Linux runners.
- Slower startup due to container build/pull.
- Defined with `runs.using: docker` and `runs.image` in `action.yml`.

### Composite Actions

- Combine multiple steps (shell commands and other actions) into a single action.
- Defined with `runs.using: composite` in `action.yml`.
- Each step must specify a `shell` when using `run`.
- Great for reusing common step sequences without writing JavaScript or Docker.

### action.yml Metadata

- Every action requires an `action.yml` (or `action.yaml`) file at the root.
- Key fields: `name`, `description`, `inputs`, `outputs`, `runs`.
- Inputs can have `description`, `required`, and `default` properties.
- Branding fields (`icon`, `color`) control the Marketplace appearance.

### Inputs and Outputs

- Inputs are passed to the action via the `with` key in the calling workflow.
- Access inputs in JavaScript with `core.getInput('name')` or in expressions with `${{ inputs.name }}`.
- Set outputs in JavaScript with `core.setOutput('name', value)` or in composite actions with `echo "name=value" >> $GITHUB_OUTPUT`.
- Outputs enable data flow between actions and steps.

---

## Module 5: CI/CD Pipelines

### Build and Test Automation

- Use actions like `actions/setup-node`, `actions/setup-python`, `actions/setup-java` to configure language runtimes.
- Run test suites with `run` steps (e.g., `npm test`, `pytest`, `mvn test`).
- Publish test results and code-coverage reports as job summaries or PR comments.
- Fail the workflow if tests do not pass to gate merges.

### Deployment Environments

- Environments are defined in repository settings and referenced with the `environment` key in a job.
- Each environment can have its own secrets and variables.
- Environment names appear in the repository's deployment history.
- Common pattern: `staging` and `production` environments with different configurations.

### Environment Protection Rules

- **Required reviewers:** One or more people must approve before the job proceeds.
- **Wait timer:** Adds a delay (in minutes) before the job can run.
- **Deployment branches:** Restrict which branches can deploy to the environment.
- Protection rules create approval gates in your deployment pipeline.

### Deployment Strategies

- **Rolling deployment:** Deploy incrementally to subsets of targets.
- **Blue-green deployment:** Maintain two identical environments; switch traffic after validation.
- **Canary deployment:** Route a small percentage of traffic to the new version first.
- Use `concurrency` groups to prevent simultaneous deployments and enable automatic cancellation.

### Artifacts and Caching

- **Artifacts:** Use `actions/upload-artifact` and `actions/download-artifact` to share files between jobs or preserve build outputs. Retained for 90 days by default.
- **Caching:** Use `actions/cache` to cache dependencies (e.g., `node_modules`, `.pip`). Cache key is based on a hash of lock files. Caches are scoped to a branch (with fallback to the default branch). Cache size limit is 10 GB per repository.

---

## Module 6: Enterprise Management

### Organization-Level Workflows

- Store shared workflows in a central `.github` repository within the organization.
- Starter workflows help teams adopt consistent CI/CD patterns.
- Organization secrets and variables can be shared across selected repositories.
- Use repository permissions to control which repos can access shared resources.

### Runner Groups

- Group self-hosted runners to control which repositories and workflows can use them.
- Available at the organization and enterprise levels.
- Default group includes all runners; create custom groups for restricted access.
- Runner groups enable workload isolation and security boundaries.

### Self-Hosted Runners

- Install the runner application on your own infrastructure (physical, VM, container, cloud).
- Support Linux, Windows, and macOS.
- Use labels to target specific runners (e.g., `gpu`, `arm64`, `production`).
- You are responsible for patching, security, and maintenance.
- Auto-scaling can be implemented using the runner registration API or solutions like Actions Runner Controller (ARC).

### Required Workflows

- Enterprise and organization admins can enforce workflows that must run on every push or pull request.
- Required workflows run in addition to any repository-level workflows.
- Useful for enforcing compliance checks, security scans, and coding standards.
- Configured at the organization level and applied to selected repositories.

### Spending Limits

- GitHub-hosted runners consume included minutes based on your plan (Free, Pro, Team, Enterprise).
- Minute multipliers apply for Windows (2x) and macOS (10x) runners.
- Set a spending limit to cap overage charges (default is $0 -- no overage).
- Self-hosted runners do not consume GitHub-billed minutes.
- Monitor usage in the organization or enterprise billing settings.
