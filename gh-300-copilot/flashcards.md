---
layout: certification
title: "Flashcards"
cert_code: "GH-300"
cert_title: "GitHub Copilot"
cert_path: "/gh-300-copilot/"
cert_color: "#8957E5"
section: flashcards
---

# GH-300: GitHub Copilot — Flashcards

Click each term to reveal its definition.

---

<details>
<summary>GitHub Copilot</summary>

An AI-powered code assistant developed by GitHub and OpenAI that provides inline code suggestions, chat-based assistance, and CLI support. It uses large language models trained on publicly available code to predict and generate code completions based on the developer's current context.

</details>

---

<details>
<summary>Copilot Chat</summary>

An interactive conversational interface embedded in supported IDEs and on GitHub.com that allows developers to ask natural-language questions about code. It supports slash commands like `/explain`, `/tests`, `/fix`, and `/doc`, and can reference the current file, selected code, or the active workspace for context-aware responses.

</details>

---

<details>
<summary>Copilot in the CLI</summary>

A command-line interface feature that brings Copilot's AI assistance to the terminal. Developers invoke it via `gh copilot suggest` to get command suggestions or `gh copilot explain` to get explanations of shell commands. It helps construct complex CLI invocations and understand unfamiliar commands.

</details>

---

<details>
<summary>Ghost Text</summary>

The dimmed, inline text that appears in the editor as Copilot's real-time code suggestion. Ghost text shows what Copilot predicts the developer will type next. It can be accepted with `Tab`, dismissed with `Esc`, or cycled through alternatives with `Alt+]` and `Alt+[`.

</details>

---

<details>
<summary>Prompt Engineering</summary>

The practice of crafting effective inputs (comments, code context, or chat messages) to guide an AI model toward producing desired outputs. In the context of Copilot, prompt engineering involves writing clear comments, providing examples, opening relevant files for context, and iterating on prompts to improve suggestion quality.

</details>

---

<details>
<summary>Zero-Shot Prompt</summary>

A prompting technique where the developer provides only an instruction or description with no examples. Copilot relies entirely on its training data to interpret the request. Zero-shot prompts work well for common, well-known patterns but may produce generic results for specialized or ambiguous tasks.

Example: `# Write a function that reverses a string`

</details>

---

<details>
<summary>Few-Shot Prompt</summary>

A prompting technique where the developer provides one or more input/output examples before the actual request. The examples help Copilot understand the expected format, edge cases, and behavior. Few-shot prompts produce more tailored results than zero-shot prompts, especially for domain-specific or custom patterns.

Example:
```
# format_currency(1234.5) -> "$1,234.50"
# format_currency(99) -> "$99.00"
# Write the function:
```

</details>

---

<details>
<summary>Context Window</summary>

The limited amount of surrounding code that Copilot uses to generate suggestions. The context window includes content from the current file (especially code above and below the cursor) and may include content from other open tabs. It has a token limit, so excessively large files may result in truncated context. Keeping relevant code nearby improves suggestion quality.

</details>

---

<details>
<summary>Code Completion</summary>

Copilot's core feature that predicts and suggests code as the developer types. Code completions appear as ghost text in the editor and can range from a single line to entire function bodies. Copilot analyzes the current context, including comments, function signatures, and surrounding code, to generate relevant suggestions.

</details>

---

<details>
<summary>Public Code Filter</summary>

An optional Copilot setting that detects and suppresses suggestions that match publicly available code on GitHub. When enabled, suggestions that closely resemble existing public code are blocked, reducing the risk of inadvertently incorporating code with incompatible open-source licenses. It can be configured at the individual or organization level.

</details>

---

<details>
<summary>Content Exclusions</summary>

An organization-level or repository-level configuration that specifies files or directories where Copilot should not provide suggestions and should not use as context. Content exclusions use glob patterns (e.g., `secrets/**`, `*.env`) to target specific paths. This feature is available on Copilot Business and Enterprise plans and is used to protect sensitive or regulated code.

</details>

---

<details>
<summary>Copilot Business</summary>

A paid Copilot plan designed for organizations that includes all Individual features plus organization-level policy management, seat management, audit logs, content exclusions, IP indemnity, and enhanced privacy protections (no code snippet retention, no use of private code for model training). Administrators control Copilot settings across all organization members.

</details>

---

<details>
<summary>Copilot Enterprise</summary>

The most advanced Copilot plan, which includes all Business features plus Copilot knowledge bases (indexing internal documentation for chat), pull request summaries, and deeper integration with GitHub.com. Enterprise-level policies cascade down to all organizations within the enterprise, providing centralized governance for large companies.

</details>

---

<details>
<summary>Telemetry</summary>

Usage data that Copilot collects to improve the product, including suggestion acceptance rates, language usage, and feature engagement. On the Individual plan, telemetry is on by default but can be opted out. On Business and Enterprise plans, administrators can disable telemetry collection through organizational policy settings. Telemetry does not include source code on plans where code snippet retention is disabled.

</details>

---

<details>
<summary>Responsible AI</summary>

A set of principles and practices for the ethical use of AI tools in software development. In the context of GitHub Copilot, responsible AI encompasses understanding model limitations, reviewing all AI-generated code before committing, being aware of potential biases in training data, not over-relying on AI suggestions for security-sensitive code, and maintaining developer accountability for all committed code.

</details>
