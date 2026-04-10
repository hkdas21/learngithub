---
layout: certification
title: "Flashcards"
cert_code: "GH-100"
cert_title: "GitHub Administration"
cert_path: "/gh-100-administration/"
cert_color: "#28A745"
section: flashcards
---

# GitHub Administration — Flashcards

Click on each term to reveal its definition.

---

<details><summary><strong>Organization Owner</strong></summary>

The highest-privilege role within a GitHub organization. Organization Owners have complete administrative access to all repositories, teams, settings, billing, and security configurations. They can manage membership, change organization-level policies, and delete the organization. GitHub recommends having at least two Owners for continuity.
</details>

---

<details><summary><strong>Enterprise Managed Users</strong></summary>

A GitHub Enterprise Cloud feature where user accounts are provisioned, managed, and deprovisioned entirely by the enterprise's identity provider (IdP) through SCIM. EMU accounts are namespaced to the enterprise, cannot participate in public open-source projects, cannot join organizations outside the enterprise, and are fully controlled by the enterprise administrators.
</details>

---

<details><summary><strong>SAML SSO</strong></summary>

Security Assertion Markup Language Single Sign-On. A federated authentication protocol that allows organizations and enterprises to require members to authenticate through an external identity provider (such as Azure AD, Okta, or OneLogin) before accessing GitHub resources. When enabled, members must link their GitHub account to their IdP identity.
</details>

---

<details><summary><strong>SCIM</strong></summary>

System for Cross-domain Identity Management. An open standard protocol used to automate user provisioning and deprovisioning between an identity provider and GitHub. When configured, SCIM automatically creates GitHub accounts, updates attributes, and removes access when users are added to or removed from the IdP.
</details>

---

<details><summary><strong>Branch Protection Rule</strong></summary>

A repository setting that enforces specific workflows on branches matching a name pattern. Common protections include requiring pull request reviews before merging, requiring status checks to pass, enforcing signed commits, preventing force pushes, preventing branch deletion, and requiring linear commit history.
</details>

---

<details><summary><strong>Ruleset</strong></summary>

A newer, more flexible alternative to classic branch protection rules. Rulesets can be defined at the repository or organization level and apply rules to branches and tags. They support layering (multiple rulesets can apply to the same branch), bypass actors, and conditions that target specific repositories. Rulesets are the recommended approach for managing branch and tag policies at scale.
</details>

---

<details><summary><strong>CODEOWNERS</strong></summary>

A file (placed in the repository root, `docs/`, or `.github/` directory) that defines which users or teams are automatically requested as reviewers when a pull request modifies files matching specified path patterns. The last matching pattern in the file takes precedence. CODEOWNERS is enforced when branch protection requires review from code owners.
</details>

---

<details><summary><strong>Custom Repository Role</strong></summary>

An organization-level feature that allows owners to define new permission levels beyond the five built-in roles (Read, Triage, Write, Maintain, Admin). Custom roles are created by selecting a base role and adding specific additional permissions. They enable fine-grained access control that follows the principle of least privilege.
</details>

---

<details><summary><strong>Audit Log</strong></summary>

A chronological record of administrative and security-relevant actions performed within a GitHub organization or enterprise. The audit log captures events such as permission changes, repository creation and deletion, team modifications, authentication events, and policy updates. It can be searched, filtered, and exported for compliance and forensic purposes.
</details>

---

<details><summary><strong>GitHub App</strong></summary>

A first-class integration mechanism on GitHub that can act on its own behalf or on behalf of a user. GitHub Apps are installed on specific repositories or organizations, request only fine-grained permissions they need, and authenticate using private keys and installation tokens. They are the recommended way to build integrations and automations, replacing OAuth Apps for most use cases.
</details>

---

<details><summary><strong>OAuth App</strong></summary>

A legacy integration mechanism where the application acts entirely on behalf of the authorizing user, inheriting that user's full permissions across all organizations and repositories they can access. OAuth Apps do not support fine-grained permissions and are generally being superseded by GitHub Apps. They are still used in some authentication-only scenarios.
</details>

---

<details><summary><strong>Webhook</strong></summary>

An HTTP callback mechanism that sends a POST request with a JSON payload to a configured URL whenever a specified event occurs on GitHub. Webhooks can be configured at the repository, organization, or enterprise level and are used to trigger external services such as CI/CD pipelines, chat notifications, and custom automation workflows.
</details>

---

<details><summary><strong>IP Allow List</strong></summary>

A security feature available at the organization and enterprise level that restricts access to GitHub resources based on the source IP address of incoming requests. Administrators configure a list of approved IP addresses or CIDR ranges, and any request originating from an IP not on the list is denied. This is commonly used to limit access to corporate network ranges.
</details>

---

<details><summary><strong>Base Permissions</strong></summary>

The default repository permission level automatically granted to all members of a GitHub organization across all repositories. Options include None (no access), Read, Write, or Admin. Setting base permissions to the appropriate level is a key security decision: a lower default (e.g., None or Read) follows the principle of least privilege, while teams and individual grants provide additional access where needed.
</details>

---

<details><summary><strong>Outside Collaborator</strong></summary>

A person who has access to one or more repositories in an organization but is not a formal member of the organization. Outside collaborators are granted access on a per-repository basis and do not inherit the organization's base permissions. They are typically used for contractors, vendors, or external contributors who need limited access to specific projects.
</details>
