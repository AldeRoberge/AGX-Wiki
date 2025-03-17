---
tags:
  - self-hosted
  - github-actions-runner
---

**Question:**  
_I have both Windows and Linux self-hosted runners. How do I configure my GitHub Actions workflow so that it uses only the Linux runner?_

---

## Overview

By default, using only:

```yaml
runs-on: self-hosted
```

allows GitHub to choose any available self-hosted runner regardless of its operating system. To ensure that your job runs only on a Linux runner, you need to specify an additional label (in this case, `linux`).

---

## Step-by-Step Guide

### 1. Verify Runner Labels

- **Self-hosted runners** automatically get the `self-hosted` label.
- When you set up a Linux runner, GitHub usually assigns it the `linux` label by default.
- Ensure that your Linux runner has the label `linux` (you can check this under your repository or organization settings in the "Runners" section).

### 2. Update Your Workflow YAML

Modify your workflow file to include both `self-hosted` and `linux` labels in the `runs-on` attribute. This tells GitHub to queue the job only on runners that match **all** specified labels.

#### Example:

```yaml
name: Linux Build

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: [self-hosted, linux]
    steps:
      - uses: actions/checkout@v3
      - run: echo "Running on a Linux self-hosted runner"
```

### 3. Commit and Push

- Save your workflow file (e.g., `.github/workflows/build.yml`).
- Commit and push your changes to trigger the workflow.

---

- [Using self-hosted runners in a workflow](https://chatgpt.com/c/%EE%88%80cite%EE%88%82turn0search1%EE%88%81)
- [Using labels with self-hosted runners](https://chatgpt.com/c/%EE%88%80cite%EE%88%82turn0search6%EE%88%81)
