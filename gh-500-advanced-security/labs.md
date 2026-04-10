---
layout: certification
title: "Hands-On Labs"
cert_code: "GH-500"
cert_title: "GitHub Advanced Security"
cert_path: "/gh-500-advanced-security/"
cert_color: "#DA3633"
section: labs
---

# GitHub Advanced Security (GH-500) — Hands-On Labs

---

## Lab 1: Enable Secret Scanning

### Objective

Enable secret scanning on a repository, trigger an alert by committing a test secret, observe the alert lifecycle, and configure push protection.

### Steps

1. **Create a test repository.**
   - Go to GitHub and create a new **private** repository (GHAS must be available on your plan).
   - Initialize it with a README.

2. **Enable secret scanning.**
   - Navigate to **Settings > Code security and analysis**.
   - Under **Secret scanning**, click **Enable**.

3. **Commit a test secret.**
   - Create a new file (e.g., `config.txt`) with a known test pattern. GitHub provides test secrets for this purpose — use a string that matches a recognized partner pattern (e.g., a GitHub personal access token format: `ghp_` followed by 36 alphanumeric characters).
   - Commit and push the file.

4. **Observe the alert.**
   - Navigate to the **Security** tab and click **Secret scanning**.
   - You should see an alert for the committed secret.
   - Review the alert details: secret type, commit SHA, file path, and line number.
   - Dismiss the alert with the reason **Used in tests**.

5. **Configure push protection.**
   - Go back to **Settings > Code security and analysis**.
   - Under **Push protection**, click **Enable**.
   - Attempt to push another commit containing a secret. Observe the push being blocked.
   - Review the error message and the bypass options.

### Validation

- Secret scanning alert appeared in the Security tab after the initial commit.
- Push protection blocked the second push attempt.
- The alert was successfully dismissed with a reason.

---

## Lab 2: Set Up Code Scanning

### Objective

Add a CodeQL workflow to a repository, trigger a scan, and review and triage the resulting alerts.

### Steps

1. **Choose or create a repository with code.**
   - Use a repository that contains code in a supported language (JavaScript, Python, Java, etc.).
   - For learning purposes, consider forking a deliberately vulnerable repository such as **OWASP Juice Shop** or **GitHub's codeql-javascript-unsafe-jquery-plugin** demo.

2. **Add the CodeQL workflow.**
   - Navigate to the **Security** tab and click **Set up code scanning**.
   - Select the **CodeQL Analysis** starter workflow.
   - Review the generated YAML file. Note the trigger events (`push`, `pull_request`, `schedule`), the language matrix, and the autobuild step.
   - Commit the workflow file to `.github/workflows/codeql.yml`.

3. **Trigger a scan.**
   - The workflow runs automatically on the commit. Go to the **Actions** tab and watch the CodeQL workflow execute.
   - Wait for the run to complete (this may take several minutes depending on repository size).

4. **Review alerts.**
   - Navigate to **Security > Code scanning**.
   - Browse the list of alerts. Click on an alert to see:
     - The rule name and description.
     - The affected file, line number, and code snippet.
     - The severity level.
     - Data-flow paths (for path-problem queries).

5. **Triage an alert.**
   - Choose an alert and click **Dismiss alert**.
   - Select a dismissal reason (e.g., **False positive** or **Won't fix**).
   - Optionally, leave a comment explaining your decision.

### Validation

- CodeQL workflow ran successfully in the Actions tab.
- At least one code scanning alert appeared in the Security tab.
- An alert was dismissed with a reason and optional comment.

---

## Lab 3: Write a Custom CodeQL Query

### Objective

Set up the CodeQL CLI locally, write a simple custom query, and test it against a repository.

### Steps

1. **Install the CodeQL CLI.**
   - Download the CodeQL CLI bundle from the [CodeQL releases page](https://github.com/github/codeql-action/releases).
   - Extract the archive and add the `codeql` binary to your system PATH.
   - Verify installation: `codeql --version`.

2. **Create a CodeQL database.**
   - Clone a repository with JavaScript code (or your chosen language).
   - Run:
     ```bash
     codeql database create my-js-db --language=javascript --source-root=./my-repo
     ```
   - Wait for the database creation to complete.

3. **Write a custom query.**
   - Create a new file named `find-eval.ql`:
     ```ql
     /**
      * @name Find eval calls
      * @description Finds all calls to the eval() function.
      * @kind problem
      * @problem.severity warning
      * @id custom/find-eval
      */

     import javascript

     from CallExpr call
     where call.getCalleeName() = "eval"
     select call, "This code calls eval(), which can be a security risk."
     ```

4. **Run the query.**
   - Execute:
     ```bash
     codeql database analyze my-js-db find-eval.ql --format=sarif-latest --output=results.sarif
     ```
   - Review the SARIF output to see if any `eval()` calls were found.

5. **Upload results (optional).**
   - Upload the SARIF file to GitHub using the CodeQL action or the REST API to see the results as code scanning alerts.

### Validation

- CodeQL CLI installed and `codeql --version` outputs the version.
- Database was created successfully.
- Query executed without errors and produced SARIF output.
- Results (if any) correctly identify `eval()` calls.

---

## Lab 4: Configure Dependabot

### Objective

Enable the dependency graph, configure Dependabot for both security updates and version updates, and review the generated pull requests.

### Steps

1. **Enable the dependency graph.**
   - Navigate to **Settings > Code security and analysis**.
   - Ensure the **Dependency graph** is enabled (it is on by default for public repos).

2. **Enable Dependabot alerts.**
   - On the same settings page, enable **Dependabot alerts**.

3. **Enable Dependabot security updates.**
   - Enable **Dependabot security updates**. Dependabot will now automatically create PRs for vulnerable dependencies.

4. **Configure Dependabot version updates.**
   - Create the file `.github/dependabot.yml` in your repository:
     ```yaml
     version: 2
     updates:
       - package-ecosystem: "npm"
         directory: "/"
         schedule:
           interval: "weekly"
           day: "wednesday"
         open-pull-requests-limit: 5
         labels:
           - "dependencies"
           - "automated"
         commit-message:
           prefix: "deps"
     ```
   - Adjust `package-ecosystem` and `directory` to match your project.
   - Commit and push the file.

5. **Review Dependabot pull requests.**
   - Navigate to the **Pull requests** tab.
   - Look for PRs created by Dependabot (they will be labeled as configured).
   - Open a PR and review:
     - The dependency being updated and the version change.
     - The release notes and changelog included in the PR body.
     - The compatibility score (if available).
   - Merge or close the PR.

### Validation

- Dependency graph is visible under **Insights > Dependency graph**.
- Dependabot alerts appear under **Security > Dependabot**.
- At least one Dependabot version update PR was created.
- The PR includes the configured labels and commit message prefix.

---

## Lab 5: Security Overview Dashboard

### Objective

Explore the organization-level Security Overview dashboard, filter alerts by severity, and track remediation progress.

### Steps

1. **Navigate to Security Overview.**
   - Go to your **organization's page** on GitHub.
   - Click the **Security** tab at the top of the organization page.
   - You will see the **Security Overview** dashboard.

2. **Explore the overview.**
   - Review the summary cards showing:
     - Total open alerts across all repositories.
     - Alerts broken down by tool (code scanning, secret scanning, Dependabot).
     - Repositories with the most open alerts.

3. **Filter by severity.**
   - Use the severity filter to view only **critical** and **high** severity alerts.
   - Note how the repository list and alert counts change.
   - Try additional filters: by tool, by repository, by team.

4. **Drill into a repository.**
   - Click on a repository name to view its specific alerts.
   - Review the alert details and remediation options.

5. **Track remediation progress.**
   - Switch to the **Trends** or **Coverage** view (depending on your GitHub version).
   - Observe how alert counts change over time.
   - Identify repositories that have improved their security posture and those that still need attention.

6. **Export or share findings.**
   - Use the filters to create a focused view (e.g., all critical code scanning alerts).
   - Share the URL with your team — the filters are encoded in the URL.

### Validation

- Security Overview dashboard loads and shows alerts across repositories.
- Severity filters correctly narrow the displayed alerts.
- You can navigate from the overview to individual repository alerts.
- Trends or coverage data is visible for tracking remediation over time.
