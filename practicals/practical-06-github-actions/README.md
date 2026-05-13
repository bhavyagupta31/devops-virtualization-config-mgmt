# 🐳 Practical 06: GitHub Actions (CI Pipeline)

**Student:** Bhavya Gupta

---

## 🎯 Objective

To implement a Continuous Integration (CI) pipeline using GitHub Actions that automatically runs on every push to the `main` branch.

---

## 🧰 Tools Used

- GitHub Actions
- Git & GitHub

---

## 📌 Steps Performed

1. Created the workflow directory `.github/workflows/`
2. Created the workflow file `main.yml`
3. Defined the CI pipeline with three steps: checkout, list files, and print message
4. Pushed the code to the `main` branch
5. Verified the pipeline execution in the **Actions** tab on GitHub

---

## 📄 Workflow File

See [.github/workflows/main.yml](../../.github/workflows/main.yml)

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

## ✅ Output

CI pipeline executed successfully with green status. All three steps passed:
- ✅ Checkout code
- ✅ List files
- ✅ Print message

---

## 📸 Screenshot

![GitHub Actions Output](output.png)

---

## 💡 Concepts Covered

| Concept | Description |
|---------|-------------|
| Continuous Integration | Automatically build/test on every push |
| Workflow automation | YAML-based pipeline definition |
| GitHub Actions | GitHub's built-in CI/CD platform |
| Triggers | `on: push` event trigger |
| Runners | `ubuntu-latest` hosted runner |

---

## 📝 Conclusion

A CI pipeline was successfully implemented using GitHub Actions. The workflow automatically triggered on every push to `main`, ran the defined steps, and reported a green status — demonstrating the basics of continuous integration automation.
