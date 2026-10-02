# 🚀 Simple HTML CI/CD Project

A hands-on DevOps project demonstrating how a simple HTML application can be automatically validated and deployed using **GitHub Actions** and **GitHub Pages**.

The goal of this project is to understand the complete CI/CD flow — from a developer pushing code to Git, through automated validation, artifact handling, and finally deployment to a live website.

---

## 🌐 Live Application

**[View Live Application](https://saimahesh19.github.io/simple-html-cicd/)**

---

## 📌 Project Overview

This project contains a static HTML application with an automated CI/CD pipeline.

Whenever changes are pushed to the `main` branch:

```text
Developer
    │
    │ git push
    ▼
GitHub Repository
    │
    │ push event
    ▼
GitHub Actions
    │
    ├── Checkout Repository
    ├── Validate Application
    ├── Upload Website Artifact
    └── Deploy
          │
          ▼
     GitHub Pages
          │
          ▼
    Live Application
```

This demonstrates an event-driven CI/CD workflow using GitHub Actions.

---

## 🏗️ Architecture

```text
                   ┌──────────────────┐
                   │    Developer     │
                   │                  │
                   │  Code Changes    │
                   └────────┬─────────┘
                            │
                         git push
                            │
                            ▼
                   ┌──────────────────┐
                   │     GitHub       │
                   │   Repository     │
                   └────────┬─────────┘
                            │
                       Push Event
                            │
                            ▼
                 ┌──────────────────────┐
                 │   GitHub Actions     │
                 │                      │
                 │  ┌────────────────┐  │
                 │  │     Build      │  │
                 │  │                │  │
                 │  │ Checkout       │  │
                 │  │ Validate       │  │
                 │  │ Upload Artifact│  │
                 │  └───────┬────────┘  │
                 └───────────┼──────────┘
                             │
                         Build OK
                             │
                             ▼
                 ┌──────────────────────┐
                 │       Deploy         │
                 │                      │
                 │  GitHub Pages        │
                 └──────────┬───────────┘
                            │
                            ▼
                   ┌──────────────────┐
                   │  Live Website    │
                   └──────────────────┘
```

---

## ⚙️ CI/CD Workflow

The pipeline is triggered when code is pushed to the `main` branch.

### 1. Code Push

A developer makes a change to the application and pushes it:

```bash
git add .
git commit -m "Update application"
git push
```

### 2. Workflow Trigger

GitHub detects the push to `main` and starts the GitHub Actions workflow.

```yaml
on:
  push:
    branches:
      - main
```

### 3. Build Job

The build job runs on a GitHub-hosted Ubuntu runner.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

### 4. Checkout

The repository is checked out onto the runner using:

```yaml
uses: actions/checkout@v4
```

This makes the repository files available to subsequent workflow steps.

### 5. Application Validation

The workflow validates that the required HTML file exists before deployment.

```bash
test -f index.html
```

If the validation fails, the build job fails.

### 6. Artifact

The website files are packaged into an artifact that can be passed to the deployment stage.

### 7. Deployment

The deployment job runs only after the build job succeeds.

```yaml
needs: build
```

The application is then deployed to GitHub Pages.

---

## 🔄 CI/CD Dependency

One important part of this project is the dependency between CI and CD.

```text
Build
  │
  ├── Checkout
  ├── Validate
  └── Package Artifact
          │
          ▼
       Success
          │
          ▼
       Deploy
```

If the build fails:

```text
Build ❌
   │
   ▼
Deploy ⏭️ Skipped
```

This prevents an unsuccessful build from continuing to the deployment stage.

---

## 🧪 Failure Testing

The pipeline was also tested with an intentionally failing validation condition.

The purpose was to understand how GitHub Actions behaves when a CI step returns a non-zero exit code.

```text
Validation
     │
     ▼
   Failed
     │
     ▼
Build ❌
     │
     ▼
Deploy ⏭️
```

This verified that the deployment stage correctly depends on the successful completion of the build stage.

---

## 📁 Project Structure

```text
simple-html-cicd/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── index.html
│
└── README.md
```

| File         | Purpose                       |
| ------------ | ----------------------------- |
| `index.html` | Static web application        |
| `deploy.yml` | GitHub Actions CI/CD workflow |
| `README.md`  | Project documentation         |

---

## 🛠️ Technologies Used

* HTML5
* Git
* GitHub
* GitHub Actions
* YAML
* Linux / WSL
* GitHub Pages

---

## 💻 Local Development

The application can be tested locally using Python's built-in HTTP server:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

Stop the server with:

```text
Ctrl + C
```

---

## 🔧 Git Workflow Used

The project was developed using a basic Git workflow:

```text
Create Project
     ↓
git init
     ↓
Create Git Repository
     ↓
git add
     ↓
git commit
     ↓
git remote add origin
     ↓
git push
     ↓
GitHub Actions
     ↓
Deployment
```

The project also involved resolving a Git merge conflict when the local and remote repositories initially contained separate histories.

---

## 📊 Current CI/CD Flow

```text
              PUSH TO MAIN
                    │
                    ▼
           ┌─────────────────┐
           │ GitHub Actions  │
           └────────┬────────┘
                    │
                    ▼
              Build Job
                    │
          ┌─────────┴─────────┐
          │                   │
          ▼                   ▼
      Checkout            Validate
          │                   │
          └─────────┬─────────┘
                    │
                  PASS
                    │
                    ▼
            Upload Artifact
                    │
                    ▼
              Deploy Job
                    │
                    ▼
             GitHub Pages
                    │
                    ▼
              LIVE WEBSITE
```

---

## 🎯 What I Learned

Through this project, I gained hands-on understanding of:

* Creating and managing a Git repository
* Connecting a local repository to GitHub
* Git branching and remote tracking
* Handling Git merge conflicts
* Creating GitHub Actions workflows
* Understanding workflow triggers
* Understanding jobs, steps, and runners
* Using reusable GitHub Actions
* Validating application files during CI
* Working with GitHub Actions artifacts
* Creating dependencies between jobs
* Understanding CI failure behavior
* Deploying a static application using GitHub Pages
* Understanding the complete flow from `git push` to deployment

---

## 🚀 Future Improvements

The project can be extended with additional DevOps practices such as:

* Automated HTML testing
* Environment-specific deployments
* GitHub Actions secrets and variables
* Docker containerization
* Container image creation
* Deployment to a cloud platform
* Pull request-based CI
* Multiple environments such as Development and Production
* Deployment approvals
* Monitoring and health checks

---

## 👨‍💻 Project Purpose

This project was built as a **hands-on DevOps interview preparation project** to understand and demonstrate practical CI/CD concepts using GitHub Actions.

It focuses on understanding how the pipeline works rather than simply using a pre-built deployment template.

---

## 🔗 Links

**Live Application:**
https://saimahesh19.github.io/simple-html-cicd/

**GitHub Repository:**
https://github.com/saimahesh19/simple-html-cicd
