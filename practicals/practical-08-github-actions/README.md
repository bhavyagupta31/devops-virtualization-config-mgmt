# Practical 08: GitHub Actions (CI Pipeline)

**Student:** Bhavya Gupta

---

## Objective

To implement a Continuous Integration (CI) pipeline using GitHub Actions that automatically runs on every push to the `main` branch.

---

## Tools Used

- GitHub Actions
- Git & GitHub

---

## What is GitHub Actions?

GitHub Actions is a CI/CD platform built directly into GitHub. It allows you to automate workflows triggered by GitHub events such as push, pull request, or schedule. Workflows are defined in YAML files stored in `.github/workflows/`.

Key concepts:
- **Workflow** — an automated process defined in a YAML file
- **Event** — a trigger that starts the workflow (e.g., `push`, `pull_request`)
- **Job** — a set of steps that run on the same runner
- **Step** — an individual task within a job
- **Runner** — the server that executes the job (e.g., `ubuntu-latest`)
- **Action** — a reusable unit of code (e.g., `actions/checkout@v3`)

---

## Steps Performed

1. Created the workflow directory `.github/workflows/`
2. Created the workflow file `main.yml`
3. Defined the CI pipeline with three steps: checkout, list files, and print message
4. Pushed the code to the `main` branch
5. Verified the pipeline execution in the Actions tab on GitHub

---

## Workflow File

```yaml
name: DevOps CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: List files
        run: ls -la

      - name: Print message
        run: echo "CI Pipeline is working successfully!"
```

---

## Commands Used

```bash
# Stage and commit the workflow file
git add .github/workflows/main.yml
git commit -m "Add GitHub Actions CI workflow"

# Push to trigger the workflow
git push origin main
```

---

## Output

CI pipeline executed successfully with green status. All three steps passed:
- Checkout code — passed
- List files — passed
- Print message — passed

---

## Screenshot

![GitHub Actions Output](output.png)

---

## Concepts Covered

| Concept                | Description                                              |
|------------------------|----------------------------------------------------------|
| Continuous Integration | Automatically build/test on every push                   |
| Workflow automation    | YAML-based pipeline definition                           |
| GitHub Actions         | GitHub's built-in CI/CD platform                         |
| Triggers               | `on: push` event trigger                                 |
| Runners                | `ubuntu-latest` hosted runner                            |
| Actions                | Reusable steps like `actions/checkout@v3`                |

---

## Conclusion

A CI pipeline was successfully implemented using GitHub Actions. The workflow automatically triggered on every push to `main`, ran the defined steps, and reported a green status. GitHub Actions eliminates the need for a separate CI server and integrates directly with the repository.
