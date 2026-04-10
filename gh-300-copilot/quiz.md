---
layout: certification
title: "Practice Quiz"
cert_code: "GH-300"
cert_title: "GitHub Copilot"
cert_path: "/gh-300-copilot/"
cert_color: "#8957E5"
section: quiz
---

# GH-300: GitHub Copilot — Practice Quiz

Test your knowledge with these 10 practice questions. Click each question to reveal the answer and explanation.

---

### Question 1 — Responsible AI

When using GitHub Copilot, who is ultimately responsible for the quality and security of code that is committed to a repository?

A. GitHub, as the provider of Copilot
B. The AI model that generated the suggestion
C. The developer who accepts and commits the code
D. The organization's Copilot administrator

<details>
<summary>Show Answer</summary>

**C. The developer who accepts and commits the code**

Copilot is an AI assistant, not an author. The developer who accepts a suggestion and commits it bears full responsibility for ensuring the code is correct, secure, and meets quality standards. This is a core principle of responsible AI usage.

</details>

---

### Question 2 — Plan Differences

Which of the following features is available exclusively on the GitHub Copilot Enterprise plan and not on Copilot Business?

A. Organization policy management
B. Copilot Chat in the IDE
C. Copilot knowledge bases
D. Content exclusions

<details>
<summary>Show Answer</summary>

**C. Copilot knowledge bases**

Copilot knowledge bases, which allow organizations to index internal documentation for use in Copilot Chat, are an Enterprise-only feature. Organization policy management, Copilot Chat, and content exclusions are available on both Business and Enterprise plans.

</details>

---

### Question 3 — Prompt Techniques

A developer writes the following prompt for GitHub Copilot:

```python
# Example: parse_date("2024-01-15") -> {"year": 2024, "month": 1, "day": 15}
# Example: parse_date("2023-12-31") -> {"year": 2023, "month": 12, "day": 31}
# Write the function:
```

What prompting technique is being used?

A. Zero-shot prompting
B. Few-shot prompting
C. Chain-of-thought prompting
D. Retrieval-augmented generation

<details>
<summary>Show Answer</summary>

**B. Few-shot prompting**

Few-shot prompting provides one or more examples of the desired input/output before the actual request. This helps Copilot understand the expected format and behavior. Zero-shot prompting would provide only the instruction with no examples.

</details>

---

### Question 4 — Data Privacy

On GitHub Copilot Business, what happens to code snippets sent to the Copilot service for generating suggestions?

A. They are stored indefinitely for model training
B. They are retained for 30 days for quality analysis
C. They are not retained beyond what is needed to deliver the suggestion
D. They are shared with other Copilot users to improve suggestions

<details>
<summary>Show Answer</summary>

**C. They are not retained beyond what is needed to deliver the suggestion**

On the Business and Enterprise plans, GitHub does not retain code snippets after generating the suggestion, and private code is not used to train the model. This is a key privacy assurance for organizational customers.

</details>

---

### Question 5 — Content Exclusions

An organization wants to prevent GitHub Copilot from providing suggestions in files within a specific repository's `secrets/` directory. How should the administrator configure this?

A. Disable Copilot for the entire repository
B. Add a content exclusion rule with a glob pattern matching the path
C. Remove Copilot seats from developers who access that directory
D. Use a `.gitignore` entry to block Copilot from reading those files

<details>
<summary>Show Answer</summary>

**B. Add a content exclusion rule with a glob pattern matching the path**

Content exclusions allow administrators to specify repositories or file path patterns where Copilot should not provide suggestions or use files as context. Glob patterns (e.g., `secrets/**`) target specific directories without disabling Copilot across the entire repository.

</details>

---

### Question 6 — Copilot Chat Features

Which Copilot Chat slash command is used to generate unit tests for a selected block of code?

A. `/explain`
B. `/fix`
C. `/tests`
D. `/doc`

<details>
<summary>Show Answer</summary>

**C. /tests**

The `/tests` slash command in Copilot Chat generates unit tests for the selected code. `/explain` provides a code explanation, `/fix` suggests a fix for issues, and `/doc` generates documentation.

</details>

---

### Question 7 — Supported IDEs

Which of the following IDEs does GitHub Copilot support? (Select all that apply.)

A. Visual Studio Code
B. Eclipse
C. JetBrains IDEs
D. Neovim
E. Xcode

<details>
<summary>Show Answer</summary>

**A. Visual Studio Code, C. JetBrains IDEs, and D. Neovim**

GitHub Copilot is supported in Visual Studio Code, Visual Studio, JetBrains IDEs (IntelliJ, PyCharm, WebStorm, etc.), and Neovim. Eclipse and Xcode are not officially supported by GitHub Copilot.

</details>

---

### Question 8 — Code Suggestion Acceptance

A developer sees a Copilot ghost text suggestion in VS Code. Which keyboard shortcut accepts the suggestion?

A. `Enter`
B. `Tab`
C. `Ctrl+Enter`
D. `Shift+Tab`

<details>
<summary>Show Answer</summary>

**B. Tab**

Pressing `Tab` accepts the current inline (ghost text) suggestion from Copilot. `Esc` dismisses it, and `Alt+]` / `Alt+[` cycle through alternative suggestions. `Ctrl+Enter` opens the Copilot suggestions panel showing multiple alternatives.

</details>

---

### Question 9 — Telemetry Settings

An organization using Copilot Business wants to minimize data collection. Which setting should the administrator configure?

A. Disable the public code filter
B. Disable telemetry collection in the organization's Copilot policy settings
C. Remove all Copilot seats and re-add them
D. Switch from Copilot Business to Copilot Individual

<details>
<summary>Show Answer</summary>

**B. Disable telemetry collection in the organization's Copilot policy settings**

Copilot Business and Enterprise plans allow organization administrators to disable telemetry collection through the Copilot policy settings. This prevents usage data from being collected beyond what is strictly necessary for the service to function.

</details>

---

### Question 10 — Enterprise Management

An organization owner wants to enable GitHub Copilot for only two specific teams rather than the entire organization. How should they configure this?

A. Purchase individual Copilot subscriptions for each team member
B. Enable Copilot for the organization and assign seats to members of those specific teams
C. Create a separate GitHub organization for just those teams
D. Use content exclusions to block Copilot for all other teams

<details>
<summary>Show Answer</summary>

**B. Enable Copilot for the organization and assign seats to members of those specific teams**

Copilot Business and Enterprise allow granular seat management. Organization owners can enable Copilot at the organization level and then assign seats to specific individuals or teams, rather than enabling it for all members. This provides cost control and targeted rollout.

</details>
