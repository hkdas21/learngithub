---
layout: certification
title: "Hands-On Labs"
cert_code: "GH-200"
cert_title: "GitHub Actions"
cert_path: "/gh-200-actions/"
cert_color: "#F9826C"
section: labs
---

# GitHub Actions Certification (GH-200) -- Hands-On Labs

---

## Lab 1: Your First Workflow

### Objective

Create a basic GitHub Actions workflow that triggers on a push event and runs simple echo commands on a GitHub-hosted runner.

### Steps

1. Create a new GitHub repository (or use an existing test repo).
2. In the repository, create the directory structure `.github/workflows/`.
3. Create a file named `.github/workflows/ci.yml` with the following content:

```yaml
name: My First Workflow

on:
  push:
    branches:
      - main

jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - name: Say hello
        run: echo "Hello, GitHub Actions!"

      - name: Print the event name
        run: echo "This workflow was triggered by a ${{ github.event_name }} event."

      - name: Print the branch name
        run: echo "Running on branch ${{ github.ref_name }}"

      - name: List environment variables
        run: env | sort
```

4. Commit and push the file to the `main` branch.
5. Navigate to the **Actions** tab in your repository and observe the workflow run.
6. Click into the run, then into the `greet` job, and expand each step to see the output.

### Validation

- The workflow appears under the Actions tab and completes with a green checkmark.
- Each step displays the expected echo output in the logs.

---

## Lab 2: Build and Test Pipeline

### Objective

Set up a CI pipeline that checks out code, installs dependencies, runs tests, and uploads test artifacts.

### Steps

1. Initialize a project in your repository. Choose one of the following:

   **Node.js option:**
   ```bash
   npm init -y
   npm install --save-dev jest
   ```
   Create `sum.js` and `sum.test.js` with a simple function and test.

   **Python option:**
   ```bash
   echo "pytest" > requirements.txt
   ```
   Create `test_app.py` with a simple test using `pytest`.

2. Create `.github/workflows/ci.yml`:

```yaml
name: Build and Test

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test -- --ci --reporters=default --reporters=jest-junit
        env:
          JEST_JUNIT_OUTPUT_DIR: ./reports

      - name: Upload test results
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: test-results
          path: ./reports/
          retention-days: 30
```

3. Commit, push, and verify the workflow runs successfully.
4. Download the uploaded artifact from the workflow run summary page.

### Validation

- The test job passes (or fails meaningfully if a test is broken).
- The `test-results` artifact is available for download on the workflow run page.

---

## Lab 3: Matrix Strategy and Caching

### Objective

Run tests across multiple operating systems and language versions using a matrix strategy, and add dependency caching to speed up builds.

### Steps

1. Update your workflow to use a matrix strategy with caching:

```yaml
name: Matrix CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      fail-fast: false
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        node-version: [18, 20, 22]
        exclude:
          - os: macos-latest
            node-version: 18
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test
```

2. Commit and push. Observe the matrix of jobs created under the Actions tab.
3. Check the logs for cache hit/miss messages in the "Set up Node.js" step.
4. Push a second commit (no code change needed) and verify the cache is restored.

### Validation

- Multiple jobs appear in the workflow run, one per OS/version combination.
- The excluded combination (macOS + Node 18) does not appear.
- On the second run, the logs show "Cache restored successfully" or a similar cache-hit message.

---

## Lab 4: Create a Custom Action

### Objective

Build a custom composite action that can be reused across workflows and repositories.

### Steps

1. In your repository, create a directory for the action:

   ```
   .github/actions/greeting/
   ```

2. Create `.github/actions/greeting/action.yml`:

```yaml
name: 'Greeting Action'
description: 'Generates a personalized greeting message'
inputs:
  who-to-greet:
    description: 'Name of the person to greet'
    required: true
    default: 'World'
  greeting-style:
    description: 'Style of greeting (formal or casual)'
    required: false
    default: 'casual'
outputs:
  greeting:
    description: 'The generated greeting'
    value: ${{ steps.generate.outputs.greeting }}
runs:
  using: 'composite'
  steps:
    - name: Generate greeting
      id: generate
      shell: bash
      run: |
        if [ "${{ inputs.greeting-style }}" = "formal" ]; then
          GREETING="Good day, ${{ inputs.who-to-greet }}. It is a pleasure to meet you."
        else
          GREETING="Hey, ${{ inputs.who-to-greet }}! What's up?"
        fi
        echo "greeting=$GREETING" >> "$GITHUB_OUTPUT"
        echo "$GREETING"
```

3. Create a workflow that uses your custom action:

```yaml
name: Test Custom Action

on:
  workflow_dispatch:
    inputs:
      name:
        description: 'Your name'
        required: true
        default: 'Developer'

jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Run greeting action (casual)
        id: casual
        uses: ./.github/actions/greeting
        with:
          who-to-greet: ${{ github.event.inputs.name }}
          greeting-style: casual

      - name: Run greeting action (formal)
        id: formal
        uses: ./.github/actions/greeting
        with:
          who-to-greet: ${{ github.event.inputs.name }}
          greeting-style: formal

      - name: Print outputs
        run: |
          echo "Casual: ${{ steps.casual.outputs.greeting }}"
          echo "Formal: ${{ steps.formal.outputs.greeting }}"
```

4. Commit and push. Go to the Actions tab, select the workflow, and click **Run workflow**.
5. Enter a name and observe the outputs.

### Validation

- The workflow runs both greeting styles and prints the correct output for each.
- The action's outputs are accessible via the `steps` context in the consuming workflow.

---

## Lab 5: Deployment with Environments

### Objective

Configure staging and production deployment environments with approval gates and deploy an application using environment-specific settings.

### Steps

1. In your repository settings, go to **Environments** and create two environments:
   - **staging** -- no protection rules.
   - **production** -- add yourself as a required reviewer and set a 5-minute wait timer.

2. Add an environment secret to each:
   - `staging`: `DEPLOY_URL` = `https://staging.example.com`
   - `production`: `DEPLOY_URL` = `https://production.example.com`

3. Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Pipeline

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Build application
        run: echo "Building application..."

      - name: Upload build artifact
        uses: actions/upload-artifact@v4
        with:
          name: app-build
          path: .

  deploy-staging:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: staging
      url: ${{ secrets.DEPLOY_URL }}
    steps:
      - name: Download build artifact
        uses: actions/download-artifact@v4
        with:
          name: app-build

      - name: Deploy to staging
        run: |
          echo "Deploying to staging at ${{ secrets.DEPLOY_URL }}"
          echo "Deployment to staging complete."

  deploy-production:
    needs: deploy-staging
    runs-on: ubuntu-latest
    environment:
      name: production
      url: ${{ secrets.DEPLOY_URL }}
    steps:
      - name: Download build artifact
        uses: actions/download-artifact@v4
        with:
          name: app-build

      - name: Deploy to production
        run: |
          echo "Deploying to production at ${{ secrets.DEPLOY_URL }}"
          echo "Deployment to production complete."
```

4. Commit and push to `main`.
5. Watch the workflow: the `build` and `deploy-staging` jobs should run automatically. The `deploy-production` job will pause and wait for your approval.
6. After the wait timer expires, approve the deployment in the Actions UI.

### Validation

- The staging deployment runs automatically after the build job completes.
- The production deployment waits for approval before proceeding.
- Each deployment step logs the correct environment-specific `DEPLOY_URL`.
- The deployment history appears under each environment in the repository settings.
