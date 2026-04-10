---
layout: certification
title: "Practice Quiz"
cert_code: "GH-100"
cert_title: "GitHub Administration"
cert_path: "/gh-100-administration/"
cert_color: "#28A745"
section: quiz
---

# GitHub Administration — Practice Quiz

Test your knowledge with these 10 practice questions. Click on each question to reveal the answer.

---

<details><summary><strong>Q1:</strong> Which organization role has full administrative access to all repositories, teams, and settings within a GitHub organization?</summary>

**Answer:** The **Organization Owner** role. Owners can manage all aspects of the organization, including settings, billing, teams, repositories, and security configurations. This is the highest-privilege role in an organization, and GitHub recommends having at least two owners for continuity.
</details>

---

<details><summary><strong>Q2:</strong> A branch protection rule requires pull request reviews before merging. A developer pushes a new commit to an already-approved pull request. What happens to the existing approval?</summary>

**Answer:** If the **"Dismiss stale pull request approvals when new commits are pushed"** option is enabled in the branch protection rule, the existing approval is automatically dismissed and a new review is required. If this option is not enabled, the original approval remains valid even after new commits are pushed.
</details>

---

<details><summary><strong>Q3:</strong> What is an Enterprise Managed User (EMU) account, and how does it differ from a regular GitHub user account?</summary>

**Answer:** An **Enterprise Managed User** account is provisioned and fully controlled by the enterprise's identity provider (IdP) through SCIM. Unlike regular GitHub accounts, EMU accounts cannot join organizations outside the enterprise, cannot create public repositories, cannot contribute to open-source projects, and have usernames that include a short code identifying the enterprise. The enterprise has complete lifecycle control over these accounts.
</details>

---

<details><summary><strong>Q4:</strong> An organization has enabled SAML SSO. What happens when a member who has not linked their GitHub identity to the IdP tries to access the organization's private resources?</summary>

**Answer:** The member is redirected to the SAML identity provider to authenticate. They must successfully authenticate with the IdP and link their GitHub account to their IdP identity before they can access the organization's private repositories and resources. If they cannot authenticate, access is denied.
</details>

---

<details><summary><strong>Q5:</strong> Where can an organization owner view a record of administrative actions such as permission changes, repository deletions, and team modifications?</summary>

**Answer:** In the organization's **Audit log**, found under **Settings > Audit log**. The audit log records actions performed by members and administrators, including permission changes, repository events, team modifications, and authentication events. It can be searched, filtered by action type, actor, or date, and exported on supported plans.
</details>

---

<details><summary><strong>Q6:</strong> A repository has the following CODEOWNERS file. Who will be automatically requested to review a pull request that modifies a file at `/src/ui/header.tsx`?</summary>

```
* @org/backend-team
/src/ui/ @org/frontend-team
```

**Answer:** Only **@org/frontend-team** will be automatically requested for review. CODEOWNERS matches are evaluated from top to bottom, and the **last matching pattern wins**. Since `/src/ui/header.tsx` matches the `/src/ui/` pattern, the `@org/frontend-team` assignment overrides the global `*` pattern.
</details>

---

<details><summary><strong>Q7:</strong> What is the difference between the "Write" and "Maintain" repository permission levels?</summary>

**Answer:** Both **Write** and **Maintain** allow pushing to non-protected branches, managing issues, and managing pull requests. However, the **Maintain** role additionally allows managing certain repository settings (such as topics, social media preview, and wikis), managing branch protection rules (but not full admin), and triggering webhooks. **Maintain** does not include destructive admin capabilities like deleting the repository or changing its visibility.
</details>

---

<details><summary><strong>Q8:</strong> An organization wants to define a permission level that grants Write access plus the ability to manage issues and edit repository metadata, but not the ability to delete the repository. Which feature should they use?</summary>

**Answer:** **Custom repository roles**. Custom roles allow organization owners to create new permission levels by selecting a base role (e.g., Write) and adding specific additional permissions on top of it. This allows fine-grained control without granting full Admin access.
</details>

---

<details><summary><strong>Q9:</strong> How does a GitHub App differ from an OAuth App in terms of permission scope and installation?</summary>

**Answer:** A **GitHub App** is installed on specific repositories or an entire organization, acts on its own behalf (or on behalf of a user), and requests only fine-grained permissions for the specific resources it needs. An **OAuth App** acts entirely on behalf of the user who authorizes it, inheriting that user's full access level across all organizations and repositories the user can access. GitHub Apps are the recommended approach because they follow the principle of least privilege.
</details>

---

<details><summary><strong>Q10:</strong> What is the purpose of an IP allow list at the enterprise or organization level, and where is it configured?</summary>

**Answer:** An **IP allow list** restricts access to the organization's or enterprise's resources so that only requests originating from approved IP addresses or CIDR ranges are permitted. It is configured under **Organization Settings > Authentication security > IP allow list** or at the enterprise level under **Enterprise Settings > Authentication security > IP allow list**. This is commonly used to ensure that only traffic from corporate networks or VPNs can access GitHub resources.
</details>
