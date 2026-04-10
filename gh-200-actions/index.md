---
layout: certification
title: "Exam Overview"
cert_code: "GH-200"
cert_title: "GitHub Actions"
cert_path: "/gh-200-actions/"
cert_color: "#F9826C"
section: overview
---

# GitHub Actions Certification (GH-200) -- Exam Overview

## About This Certification

The GitHub Actions certification validates your skills in **automating workflows**, building **CI/CD pipelines**, creating **custom actions**, and implementing **deployment strategies** using GitHub Actions. Earning this certification demonstrates that you can design, author, and maintain workflow automation across repositories and organizations.

---

## Exam Details

| Detail             | Value                          |
|--------------------|--------------------------------|
| **Exam Code**      | GH-200                         |
| **Duration**       | 120 minutes                    |
| **Questions**      | 75                             |
| **Passing Score**  | 70%                            |
| **Format**         | Multiple choice / Multiple select |
| **Cost**           | $99 USD                        |

---

## Exam Domains

| Domain                                        | Weight |
|-----------------------------------------------|--------|
| Author and maintain workflows                 | 40%    |
| Consume workflows                             | 20%    |
| Author and maintain actions                   | 25%    |
| Manage GitHub Actions for the enterprise      | 15%    |

### Domain 1 -- Author and Maintain Workflows (40%)

This is the largest domain on the exam. You are expected to understand workflow YAML syntax, event triggers, job configuration, step definitions, runner selection, expressions, contexts, secrets management, and conditional logic.

### Domain 2 -- Consume Workflows (20%)

This domain covers finding and using existing actions from the GitHub Marketplace, referencing reusable workflows, pinning action versions, and leveraging starter workflows provided by your organization.

### Domain 3 -- Author and Maintain Actions (25%)

Expect questions on building custom JavaScript actions, Docker container actions, and composite actions. You should know how to define `action.yml` metadata, handle inputs and outputs, and publish actions to the Marketplace.

### Domain 4 -- Manage GitHub Actions for the Enterprise (15%)

This domain focuses on organization-level workflow management, runner groups, self-hosted runners, required workflows, spending limits, and policies that govern Actions usage across an enterprise.

---

## Preparation Tips

1. **Master YAML syntax.** Nearly every exam question involves reading or writing YAML. Be comfortable with mappings, sequences, multi-line strings, and anchors.
2. **Know your workflow triggers inside and out.** Understand the differences between `push`, `pull_request`, `workflow_dispatch`, `schedule`, `repository_dispatch`, and event filtering with branches, tags, and paths.
3. **Practice hands-on.** Create real workflows in a test repository. There is no substitute for writing and debugging YAML yourself.
4. **Study the expression and context syntax.** Learn how to use `${{ }}` expressions, the `github`, `env`, `secrets`, `steps`, `jobs`, and `runner` contexts, and status-check functions like `success()`, `failure()`, and `always()`.
5. **Understand security best practices.** Know how `GITHUB_TOKEN` permissions work, how to use environments with protection rules, and how to handle secrets safely.
6. **Review the official GitHub Actions documentation.** The exam draws heavily from the docs at [docs.github.com/en/actions](https://docs.github.com/en/actions).
