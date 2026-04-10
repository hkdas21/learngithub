---
layout: certification
title: "Hands-on Labs"
cert_code: "GH-100"
cert_title: "GitHub Administration"
cert_path: "/gh-100-administration/"
cert_color: "#28A745"
section: labs
---

# GitHub Administration — Hands-on Labs

---

## Lab 1: Configure Organization Settings

### Objective

Create a new GitHub organization and configure its core settings, including base permissions, member privileges, and verified domains.

### Steps

1. Navigate to **github.com** and click the **+** menu in the top-right corner. Select **New organization**.
2. Choose the **Free** plan (or Team if available) and provide an organization name such as `gh100-lab-org`. Complete the creation wizard.
3. Go to **Settings > Member privileges**. Set the base permission for all repositories to **Read**. This ensures members can view all repos by default but cannot push changes.
4. Under **Member privileges**, disable the ability for members to create public repositories. Leave private repository creation enabled.
5. Navigate to **Settings > Verified & approved domains**. Add your organization's domain (e.g., `example.com`) and follow the DNS TXT record verification steps.
6. Go to **Settings > Profile** and fill in the organization display name, description, URL, and location.
7. Navigate to **Settings > Authentication security**. Review the options for requiring 2FA for organization members. Enable this setting if you are working with a test organization.

### Verification

- Confirm the base permission is set to **Read** by checking **Settings > Member privileges**.
- Verify that public repository creation is disabled for members.
- Confirm the domain shows as **Verified** under the domains settings.
- Invite a test user (or use an alt account) and confirm they receive read-only access to existing repositories.

---

## Lab 2: Manage Teams and Access

### Objective

Create teams within the organization, assign repository access at the team level, and configure a CODEOWNERS file to automate review assignments.

### Steps

1. In your organization, navigate to **Teams** and click **New team**. Create a team named `backend-team` with **Visible** visibility and a description of "Backend engineers."
2. Create a second team named `frontend-team` with **Visible** visibility.
3. Optionally, create a parent team named `engineering` and nest both `backend-team` and `frontend-team` under it.
4. Create a new repository called `gh100-lab-repo` in the organization. Initialize it with a README.
5. Go to the repository **Settings > Collaborators and teams**. Add `backend-team` with **Write** access and `frontend-team` with **Read** access.
6. In the repository, create a file named `CODEOWNERS` in the root directory (or in the `.github/` directory) with the following content:
   ```
   # Default owners for everything
   * @gh100-lab-org/backend-team

   # Frontend team owns the UI directory
   /src/ui/ @gh100-lab-org/frontend-team

   # Docs owned by the whole engineering team
   /docs/ @gh100-lab-org/engineering
   ```
7. Commit the CODEOWNERS file to the default branch.

### Verification

- Navigate to the **Teams** tab and confirm both teams exist with correct visibility.
- On the repository settings page, verify that `backend-team` has **Write** access and `frontend-team` has **Read** access.
- Create a test pull request that modifies a file in `/src/ui/`. Confirm that `frontend-team` is automatically requested for review.
- If nested teams were created, verify that the parent team `engineering` appears in the teams list and the children are nested beneath it.

---

## Lab 3: Enforce Branch Protection

### Objective

Set up branch protection rules on the default branch to require pull request reviews, enforce status checks, and prevent force pushes.

### Steps

1. In the `gh100-lab-repo` repository, navigate to **Settings > Branches**.
2. Click **Add branch protection rule** (or **Add classic branch protection rule** if rulesets are the default).
3. Set the **Branch name pattern** to `main`.
4. Enable **Require a pull request before merging**. Set the required number of approving reviews to **1**.
5. Check **Dismiss stale pull request approvals when new commits are pushed**.
6. Enable **Require status checks to pass before merging**. In the search box, add a status check name such as `ci/build` (you can configure this later with an actual CI workflow).
7. Check **Require branches to be up to date before merging**.
8. Enable **Restrict who can push to matching branches**. Add only the `backend-team` as an allowed actor.
9. Enable **Do not allow force pushes**.
10. Enable **Do not allow deletions**.
11. Click **Create** to save the branch protection rule.

### Verification

- Navigate to **Settings > Branches** and confirm the protection rule is listed for `main`.
- Attempt to push directly to `main` from the command line. Confirm the push is rejected.
- Create a pull request targeting `main`. Verify that at least one approval is required before the merge button becomes active.
- Confirm that the force push and deletion restrictions are displayed in the rule summary.

---

## Lab 4: Audit and Compliance

### Objective

Explore the organization audit log, set up a webhook for event notifications, and review security settings relevant to compliance.

### Steps

1. Navigate to your organization's **Settings > Audit log**.
2. In the search bar, enter `action:org.update_member_repository_creation_permission` to filter for events related to the member privilege change you made in Lab 1. Review the event details.
3. Experiment with other audit log filters:
   - `action:repo.create` to see repository creation events.
   - `actor:<your-username>` to see all actions performed by your account.
   - `created:>2026-04-01` to see events from the past week.
4. Click **Export** (if available on your plan) to download audit log data as JSON or CSV.
5. Navigate to **Settings > Webhooks**. Click **Add webhook**.
6. Set the **Payload URL** to a testing endpoint such as `https://webhook.site` (generate a unique URL from that service).
7. Set **Content type** to `application/json`.
8. Under **Which events would you like to trigger this webhook?**, select **Let me select individual events**. Choose:
   - **Repositories** (to be notified when repos are created, deleted, or archived)
   - **Members** (to be notified when membership changes)
   - **Teams** (to be notified when teams are modified)
9. Click **Add webhook** to save.
10. Navigate to **Settings > Code security and analysis**. Review the available security features (Dependabot alerts, secret scanning, push protection) and enable any that are relevant.

### Verification

- Confirm audit log queries return expected results for organization actions you performed earlier.
- On the webhook testing endpoint, trigger an event (e.g., create a new repository) and verify that the webhook payload is received.
- Check the webhook delivery log under **Settings > Webhooks > Recent Deliveries** to confirm a `200` response.
- Confirm that security features (Dependabot, secret scanning) are enabled as expected.

---

## Lab 5: Automate with GitHub Apps

### Objective

Create a simple GitHub App, configure its permissions and event subscriptions, and install it on your organization.

### Steps

1. Navigate to **Settings > Developer settings > GitHub Apps** (from your personal account settings). Click **New GitHub App**.
2. Fill in the required fields:
   - **GitHub App name:** `gh100-lab-admin-app` (must be globally unique; add a suffix if needed).
   - **Homepage URL:** `https://example.com`.
   - **Webhook URL:** Use a testing endpoint such as `https://webhook.site` with a unique URL, or uncheck **Active** under the Webhook section if you do not need real-time events for this lab.
3. Under **Permissions**, configure the following:
   - **Repository permissions:**
     - **Contents:** Read-only
     - **Issues:** Read & write
     - **Pull requests:** Read-only
   - **Organization permissions:**
     - **Members:** Read-only
4. Under **Subscribe to events**, check:
   - **Issues**
   - **Pull request**
5. Under **Where can this GitHub App be installed?**, select **Only on this account**.
6. Click **Create GitHub App**.
7. On the app settings page, note the **App ID** and generate a **Private key** (download the `.pem` file).
8. Navigate to **Install App** in the left sidebar. Click **Install** next to your organization.
9. Choose **All repositories** or select specific repositories (e.g., `gh100-lab-repo`). Click **Install**.

### Verification

- Navigate to your organization's **Settings > Installed GitHub Apps** and confirm the app appears in the list.
- Verify the app's permissions by clicking on **Configure** next to the installed app. Confirm that Contents (read), Issues (read/write), and Pull requests (read) are listed.
- Create a test issue in `gh100-lab-repo`. If the webhook is active, confirm the event payload is received at the webhook URL.
- Confirm the private key `.pem` file was downloaded. This key would be used to authenticate the app in production automation scripts.
