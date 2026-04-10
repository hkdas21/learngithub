---
layout: certification
title: "Study Notes"
cert_code: "GH-100"
cert_title: "GitHub Administration"
cert_path: "/gh-100-administration/"
cert_color: "#28A745"
section: study-notes
---

# GitHub Administration — Study Notes

---

## Module 1: Managing User Access (20%)

### Key Topics

- **Organization roles:** Owner, Member, Billing Manager, Outside Collaborator
- **Repository permission levels:** Read, Triage, Write, Maintain, Admin
- **SSO and SAML:** Configuring SAML single sign-on for an organization, linking identities, enforcing SSO
- **SCIM provisioning:** Automatically syncing user accounts from an identity provider (IdP) to GitHub
- **2FA enforcement:** Requiring two-factor authentication for all organization members and outside collaborators

### Outline

1. Identify the built-in organization roles and what each can do
2. Explain how repository permission levels map to specific capabilities (push, merge, manage settings)
3. Configure SAML SSO with an identity provider (Azure AD, Okta, OneLogin)
4. Enable SCIM provisioning to automate user lifecycle management
5. Enforce 2FA across the organization and handle non-compliant members

<!-- TODO: Add detailed notes on SAML SSO configuration steps -->
<!-- TODO: Add detailed notes on SCIM provisioning troubleshooting -->
<!-- TODO: Add comparison table of organization roles and their capabilities -->

---

## Module 2: Managing Repository Activity (15%)

### Key Topics

- **Branch protection rules:** Required reviews, status checks, signed commits, linear history
- **Rulesets:** Organization-level and repository-level rulesets as a modern alternative to branch protection
- **CODEOWNERS:** Defining code ownership for automatic review assignment
- **Merge strategies:** Merge commit, squash merge, rebase merge — when to use each
- **Archiving repositories:** When and how to archive repos, and what archiving restricts

### Outline

1. Create and configure branch protection rules for the default branch
2. Set up rulesets that apply across multiple repositories in an organization
3. Write a CODEOWNERS file with team-based and path-based ownership rules
4. Choose and enforce appropriate merge strategies for different repositories
5. Archive inactive repositories and understand the read-only restrictions

<!-- TODO: Add detailed notes on ruleset bypass actors and conditions -->
<!-- TODO: Add example CODEOWNERS file with annotations -->
<!-- TODO: Add comparison of branch protection vs. rulesets -->

---

## Module 3: Managing GitHub Organization Settings (20%)

### Key Topics

- **Organization profile:** Display name, description, URL, verified domains
- **Member privileges:** Repository creation permissions, forking policy, Pages visibility
- **Base permissions:** Default permission level granted to all organization members on all repositories
- **Billing:** Understanding GitHub plans (Free, Team, Enterprise), seat management, usage-based billing
- **Audit log:** Viewing, searching, filtering, and exporting audit log events

### Outline

1. Configure the organization profile and verify a custom domain
2. Set member privileges to control what members can create and access by default
3. Choose an appropriate base permission level (None, Read, Write, Admin)
4. Manage billing, add seats, and understand plan differences
5. Use the audit log to investigate user actions, permission changes, and security events

<!-- TODO: Add detailed notes on audit log event categories and search syntax -->
<!-- TODO: Add detailed notes on verified domains and email restrictions -->
<!-- TODO: Add billing comparison table across GitHub plans -->

---

## Module 4: Managing Team Policies (15%)

### Key Topics

- **Team creation:** Creating teams, setting descriptions, and choosing visibility (visible or secret)
- **Nested teams:** Parent-child team hierarchies and permission inheritance
- **Team sync with IdP:** Automatically syncing team membership from identity provider groups
- **Team-level permissions:** Granting teams read, triage, write, maintain, or admin access to repositories

### Outline

1. Create teams with appropriate naming conventions and visibility settings
2. Build nested team hierarchies where child teams inherit parent permissions
3. Configure team sync with an identity provider to automate membership
4. Assign repository access to teams rather than individual users
5. Use team mentions and CODEOWNERS to integrate teams into the review workflow

<!-- TODO: Add detailed notes on team sync supported IdPs and configuration -->
<!-- TODO: Add best practices for team naming conventions -->
<!-- TODO: Add diagram of nested team permission inheritance -->

---

## Module 5: Administering GitHub Enterprise (15%)

### Key Topics

- **GHEC vs. GHES:** Differences between GitHub Enterprise Cloud and GitHub Enterprise Server
- **Enterprise Managed Users (EMU):** Centrally managed user accounts provisioned entirely by the enterprise IdP
- **IP allow lists:** Restricting access to enterprise and organization resources by IP address
- **Enterprise policies:** Setting policies at the enterprise level that apply to all organizations

### Outline

1. Compare GHEC and GHES deployment models, features, and use cases
2. Explain Enterprise Managed Users — how they differ from regular accounts, what they can and cannot do
3. Configure IP allow lists at the enterprise and organization levels
4. Set enterprise-level policies for repository creation, forking, visibility changes, and more
5. Manage multiple organizations under a single enterprise account

<!-- TODO: Add detailed notes on EMU limitations and identity provider requirements -->
<!-- TODO: Add GHEC vs. GHES feature comparison table -->
<!-- TODO: Add detailed notes on enterprise policy inheritance -->

---

## Module 6: Managing GitHub at Scale (15%)

### Key Topics

- **Custom repository roles:** Defining roles beyond the five built-in levels with specific fine-grained permissions
- **GitHub Apps:** Creating and managing GitHub Apps for automation, integrations, and CI/CD
- **Webhooks:** Configuring repository, organization, and enterprise webhooks to trigger external services
- **API automation:** Using the GitHub REST API and GraphQL API to manage resources programmatically

### Outline

1. Create custom repository roles with tailored permission sets
2. Build and install GitHub Apps with appropriate permissions and event subscriptions
3. Configure webhooks at the repository, organization, and enterprise levels
4. Use the REST API to automate repetitive administrative tasks (e.g., creating repos, managing teams)
5. Use the GraphQL API for efficient bulk queries and mutations

<!-- TODO: Add detailed notes on custom role permission options -->
<!-- TODO: Add example GitHub App manifest and installation steps -->
<!-- TODO: Add example webhook payload and delivery troubleshooting -->
<!-- TODO: Add example API scripts for common admin tasks -->
