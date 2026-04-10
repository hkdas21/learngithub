---
layout: certification
title: "Quiz"
cert_code: "GH-900"
cert_title: "GitHub Foundations"
cert_path: "/gh-900-foundations/"
cert_color: "#2088FF"
section: quiz
---

## Practice Quiz

Test your knowledge with these practice questions. Click on each question to reveal the answer.

---

<details>
<summary><strong>Q1:</strong> What type of version control system is Git?</summary>

**Answer: Distributed Version Control System (DVCS)**

Unlike centralized systems (e.g., SVN), every developer has a full copy of the repository history locally. This means you can commit, branch, and merge without a network connection.
</details>

<details>
<summary><strong>Q2:</strong> What is the difference between a fork and a clone?</summary>

**Answer:**
- **Fork**: Creates a copy of the repository under your GitHub account (server-side). Used for contributing to others' projects.
- **Clone**: Creates a local copy of a repository on your machine. Used for local development.
</details>

<details>
<summary><strong>Q3:</strong> Which merge strategies are available for pull requests on GitHub? (Select all that apply)</summary>

**Answer: Merge commit, Squash and merge, Rebase and merge**

- **Merge commit**: Preserves all commits and creates a merge commit
- **Squash and merge**: Combines all commits into a single commit
- **Rebase and merge**: Replays commits on top of the base branch
</details>

<details>
<summary><strong>Q4:</strong> What file specifies the individuals or teams responsible for code in a repository?</summary>

**Answer: CODEOWNERS**

The `CODEOWNERS` file (placed in the root, `.github/`, or `docs/` directory) automatically requests reviews from the designated owners when a pull request modifies their code.
</details>

<details>
<summary><strong>Q5:</strong> What is GitHub Codespaces?</summary>

**Answer:** A cloud-based development environment hosted by GitHub. It provides a fully configured VS Code instance in the browser (or connected to your local VS Code) with compute, storage, and pre-configured dev containers.
</details>

<details>
<summary><strong>Q6:</strong> How do you automatically close an issue when a pull request is merged?</summary>

**Answer:** Use a closing keyword in the pull request description or commit message, such as:
- `Closes #123`
- `Fixes #123`
- `Resolves #123`
</details>

<details>
<summary><strong>Q7:</strong> What is the purpose of a .gitignore file?</summary>

**Answer:** The `.gitignore` file specifies files and directories that Git should ignore and not track. Common entries include `node_modules/`, `.env`, build output directories, and OS-specific files like `.DS_Store`.
</details>

<details>
<summary><strong>Q8:</strong> What are GitHub Actions?</summary>

**Answer:** GitHub Actions is a CI/CD platform that allows you to automate build, test, and deployment pipelines. Workflows are defined in YAML files stored in `.github/workflows/` and triggered by events like pushes, pull requests, or schedules.
</details>

<details>
<summary><strong>Q9:</strong> What is the difference between a public and private repository?</summary>

**Answer:**
- **Public**: Visible to everyone on the internet. Anyone can see the code but only collaborators can push.
- **Private**: Only visible to the owner and explicitly added collaborators.
</details>

<details>
<summary><strong>Q10:</strong> What is GitHub Discussions used for?</summary>

**Answer:** GitHub Discussions provides a forum-like space within a repository for community conversations, Q&A, announcements, and brainstorming. Unlike issues, discussions are not tracked as work items.
</details>

---

<!-- Add more questions as you study each module -->
