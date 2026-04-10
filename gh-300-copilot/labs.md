---
layout: certification
title: "Hands-On Labs"
cert_code: "GH-300"
cert_title: "GitHub Copilot"
cert_path: "/gh-300-copilot/"
cert_color: "#8957E5"
section: labs
---

# GH-300: GitHub Copilot — Hands-On Labs

---

## Lab 1: Set Up GitHub Copilot

### Objective

Install the GitHub Copilot extension in VS Code, sign in with your GitHub account, and configure basic settings to prepare your development environment.

### Prerequisites

- A GitHub account with an active Copilot subscription (Individual, Business, or Enterprise)
- Visual Studio Code installed (latest stable version)

### Steps

1. **Install the GitHub Copilot extension.**
   - Open VS Code.
   - Go to the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`).
   - Search for "GitHub Copilot" and click **Install**.
   - Also install "GitHub Copilot Chat" for the chat interface.

2. **Sign in to GitHub.**
   - After installation, a prompt appears to sign in to GitHub.
   - Click **Sign in to GitHub** and complete the OAuth flow in your browser.
   - Return to VS Code and confirm that the Copilot icon appears in the status bar.

3. **Configure Copilot settings.**
   - Open VS Code Settings (`Ctrl+,` / `Cmd+,`).
   - Search for "Copilot" to see all available settings.
   - Review and configure the following:
     - **Enable/Disable for specific languages:** Toggle Copilot on or off for individual languages.
     - **Inline suggestions:** Ensure inline suggestions are enabled.
     - **Public code filter:** Enable if you want to filter out matches to public code.
   - Save your settings.

4. **Verify Copilot is working.**
   - Create a new file called `hello.py`.
   - Type the following comment and press `Enter`:
     ```python
     # Write a function that greets a user by name
     ```
   - Observe that Copilot provides a ghost text suggestion.
   - Press `Tab` to accept the suggestion.

### Validation

- The Copilot icon in the status bar shows an active state (no warning or error icon).
- Ghost text suggestions appear when you type code or comments.
- You can open the Copilot Chat panel and send a message without errors.

---

## Lab 2: Effective Prompt Engineering

### Objective

Practice writing comments and prompts that guide Copilot toward accurate and useful code suggestions. Compare zero-shot and few-shot prompting techniques.

### Prerequisites

- Completed Lab 1 (Copilot installed and active)

### Steps

1. **Zero-shot prompting.**
   - Create a new file called `prompts_zero.py`.
   - Write the following comment and let Copilot generate the function:
     ```python
     # Write a function that checks if a string is a palindrome
     ```
   - Accept the suggestion and review the generated code.
   - Note the approach Copilot chose (e.g., string reversal, two-pointer).

2. **Few-shot prompting.**
   - Create a new file called `prompts_few.py`.
   - Provide examples before your request:
     ```python
     # Examples:
     # is_palindrome("racecar") -> True
     # is_palindrome("hello") -> False
     # is_palindrome("A man a plan a canal Panama") -> True  (ignore spaces and case)
     #
     # Write the function:
     ```
   - Accept the suggestion and review the generated code.
   - Compare with the zero-shot result. The few-shot version should handle case insensitivity and spaces because the examples made that expectation explicit.

3. **Iterative refinement.**
   - In a new file called `prompts_refined.py`, start with a vague prompt:
     ```python
     # sort a list
     ```
   - Review the suggestion. It may be generic.
   - Now refine the prompt with more detail:
     ```python
     # Sort a list of dictionaries by the "last_name" key in ascending order,
     # with a secondary sort by "first_name" in case of ties.
     # Return a new list without modifying the original.
     ```
   - Compare the two suggestions and note how specificity improves output quality.

4. **Comment-driven development.**
   - In a new file called `prompts_comments.py`, write a structured comment block:
     ```python
     # Function: calculate_shipping_cost
     # Parameters:
     #   - weight_kg (float): package weight in kilograms
     #   - distance_km (float): shipping distance in kilometers
     #   - express (bool): whether to use express shipping (2x cost)
     # Returns:
     #   - float: total shipping cost
     # Rules:
     #   - Base rate: $0.50 per kg per 100 km
     #   - Minimum charge: $5.00
     #   - Express doubles the total cost
     ```
   - Let Copilot generate the implementation from this comment.

### Validation

- The few-shot prompt produces a more tailored result than the zero-shot prompt.
- The refined prompt generates a significantly better suggestion than the vague prompt.
- The comment-driven approach produces a function that matches the specified rules.

---

## Lab 3: Code Generation Workflow

### Objective

Use GitHub Copilot to build a small REST API, practicing the workflow of generating, reviewing, and refining AI-suggested code.

### Prerequisites

- Completed Labs 1 and 2
- Node.js installed (v18+)
- Familiarity with Express.js basics

### Steps

1. **Initialize the project.**
   - Create a new directory and initialize a Node.js project:
     ```bash
     mkdir copilot-api && cd copilot-api
     npm init -y
     npm install express
     ```
   - Open the directory in VS Code.

2. **Generate the server scaffold.**
   - Create a file called `server.js`.
   - Write the following comment at the top:
     ```javascript
     // Express REST API server for managing a to-do list
     // Endpoints:
     //   GET    /todos       - list all todos
     //   POST   /todos       - create a new todo
     //   GET    /todos/:id   - get a single todo by ID
     //   PUT    /todos/:id   - update a todo by ID
     //   DELETE /todos/:id   - delete a todo by ID
     // Store todos in memory using an array
     ```
   - Let Copilot generate the server code. Accept suggestions incrementally, reviewing each endpoint.

3. **Review and refine.**
   - After the initial generation, review the code for:
     - Proper HTTP status codes (201 for creation, 404 for not found, etc.)
     - Input validation (does it check for missing fields?)
     - Consistent response format
   - Use Copilot Chat to ask: "Review this Express server for best practices and suggest improvements."
   - Apply the suggested improvements.

4. **Add middleware.**
   - Write a comment requesting error-handling middleware:
     ```javascript
     // Add error-handling middleware that catches errors and returns
     // a JSON response with the error message and a 500 status code
     ```
   - Let Copilot generate the middleware and integrate it into the server.

5. **Test the API.**
   - Start the server: `node server.js`
   - Use `curl` or a tool like Postman to test each endpoint.
   - Verify correct behavior for both valid and invalid requests.

### Validation

- The server starts without errors and listens on the specified port.
- All five CRUD endpoints return appropriate status codes and response bodies.
- The error-handling middleware catches and formats errors correctly.

---

## Lab 4: Generate Tests with Copilot

### Objective

Use Copilot Chat to generate unit tests for existing functions, exploring how Copilot handles different testing scenarios.

### Prerequisites

- Completed Labs 1 through 3
- Python 3.8+ with `pytest` installed (`pip install pytest`)

### Steps

1. **Create functions to test.**
   - Create a file called `utils.py` with the following functions:
     ```python
     def celsius_to_fahrenheit(celsius):
         """Convert Celsius to Fahrenheit."""
         return (celsius * 9 / 5) + 32

     def find_duplicates(items):
         """Return a list of duplicate items in the input list."""
         seen = set()
         duplicates = set()
         for item in items:
             if item in seen:
                 duplicates.add(item)
             seen.add(item)
         return list(duplicates)

     def truncate_string(text, max_length, suffix="..."):
         """Truncate a string to max_length and append suffix if truncated."""
         if len(text) <= max_length:
             return text
         return text[: max_length - len(suffix)] + suffix
     ```

2. **Generate tests using Copilot Chat.**
   - Select the `celsius_to_fahrenheit` function.
   - Open Copilot Chat and type: `/tests Generate pytest tests for this function, including edge cases like 0, 100, -40, and negative values.`
   - Review the generated tests. Copy them into a new file called `test_utils.py`.

3. **Generate tests for remaining functions.**
   - Repeat the process for `find_duplicates`:
     - `/tests Generate pytest tests including empty list, no duplicates, multiple duplicates, and mixed types.`
   - Repeat for `truncate_string`:
     - `/tests Generate pytest tests including strings shorter than max_length, exact length, and custom suffix.`

4. **Run the tests.**
   - Execute: `pytest test_utils.py -v`
   - Review the results. Fix any failing tests by examining whether the test expectation or the function implementation is incorrect.

5. **Ask for edge cases you may have missed.**
   - In Copilot Chat, ask: "What edge cases am I missing in my tests for these three functions?"
   - Add any valuable suggestions to your test file and re-run.

### Validation

- All generated tests pass when run with `pytest`.
- The test suite covers standard cases, boundary cases, and at least two edge cases per function.
- You can articulate which tests Copilot generated well and which needed manual adjustment.

---

## Lab 5: Copilot Chat for Code Review

### Objective

Use Copilot Chat to explain unfamiliar code, identify potential bugs, and suggest refactoring improvements.

### Prerequisites

- Completed Labs 1 through 4

### Steps

1. **Explain unfamiliar code.**
   - Create a file called `review_me.py` with the following code:
     ```python
     def f(n):
         a, b = 0, 1
         r = []
         while a < n:
             r.append(a)
             a, b = b, a + b
         return r

     def g(d, k, default=None):
         keys = k.split(".")
         current = d
         for key in keys:
             if isinstance(current, dict) and key in current:
                 current = current[key]
             else:
                 return default
         return current
     ```
   - Select function `f` and use Copilot Chat: `/explain What does this function do?`
   - Select function `g` and repeat. Verify that Copilot correctly identifies the purpose of each function.

2. **Find bugs.**
   - Create a file called `buggy.py`:
     ```python
     def average(numbers):
         total = 0
         for num in numbers:
             total += num
         return total / len(numbers)

     def get_initials(name):
         parts = name.split(" ")
         initials = ""
         for part in parts:
             initials += part[0].upper()
         return initials
     ```
   - Select all the code and ask Copilot Chat: "Find potential bugs or issues in this code."
   - Expected issues: `average` will raise `ZeroDivisionError` on an empty list; `get_initials` will raise `IndexError` if there are extra spaces causing empty strings in the split result.

3. **Suggest refactoring.**
   - Create a file called `refactor_me.py`:
     ```python
     def process_order(order):
         if order["status"] == "pending":
             if order["total"] > 100:
                 if order["customer"]["is_premium"]:
                     discount = 0.2
                 else:
                     discount = 0.1
             else:
                 if order["customer"]["is_premium"]:
                     discount = 0.1
                 else:
                     discount = 0.0
             order["total"] = order["total"] * (1 - discount)
             order["status"] = "processed"
         return order
     ```
   - Select the function and ask Copilot Chat: "Refactor this function to reduce nesting and improve readability."
   - Review the suggested refactoring. Apply it if it improves clarity.

4. **Compare before and after.**
   - For each refactoring suggestion, verify that the behavior is preserved by writing a quick test or running the original and refactored versions with the same inputs.

### Validation

- Copilot Chat correctly explains the purpose of functions `f` (Fibonacci sequence) and `g` (nested dictionary key lookup).
- Copilot identifies the division-by-zero and index-error bugs.
- The refactored `process_order` function has reduced nesting and produces the same output as the original.
