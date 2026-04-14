# ⚙️ DevOps Home Lab — Project 3: CI/CD Pipeline (GitHub Actions)
## Author: Chip Sineath | DevOps Home Lab

A production-grade CI/CD pipeline written in GitHub Actions YAML. Every single line is commented so you understand exactly what it does and why.

## ⚠️ IMPORTANT: How to Use This File
The workflow file is at `workflows/deploy.yml` in this repo.

In a real project, copy it to `.github/workflows/deploy.yml` in your repository. GitHub Actions only reads workflow files from the `.github/workflows/` directory.

```bash
# In your actual project repo:
mkdir -p .github/workflows
cp deploy.yml .github/workflows/deploy.yml
git add .github/
git commit -m "feat: add CI/CD pipeline"
git push
```

## What This Pipeline Does
Every time you push code to `main`, it automatically:
1. **Lints** — checks for syntax errors and hardcoded secrets
2. **Tests** — runs on Node.js 18, 20, and 22 simultaneously (matrix builds)
3. **Builds** — creates a Docker image and pushes to Docker Hub
4. **Deploys** — SSH into your server and runs the new container

## What You'll Learn
| Concept | Where It Appears |
|---|---|
| YAML syntax | The entire file |
| Triggers (when to run) | `on:` block |
| Jobs and steps | `jobs:` block |
| Matrix builds | `strategy.matrix` |
| GitHub Secrets | `${{ secrets.NAME }}` |
| Docker build + push | `docker/build-push-action` |
| SSH deployment | `appleboy/ssh-action` |
| Conditional execution | `if: github.ref == ...` |

## Required GitHub Secrets
Set these in: **Settings → Secrets and variables → Actions**

| Secret Name | What It Is |
|---|---|
| `DOCKERHUB_USERNAME` | Your Docker Hub username |
| `DOCKERHUB_TOKEN` | Docker Hub access token (not your password) |
| `SERVER_HOST` | Your server's IP address |
| `SERVER_USER` | SSH username (usually `ubuntu`) |
| `SERVER_SSH_KEY` | Content of your `~/.ssh/id_rsa` private key |

## Study Path
1. Read `workflows/deploy.yml` top to bottom — every line is commented
2. Create a test repo and add this workflow
3. Push a commit and watch it run in the GitHub Actions tab
4. Break something on purpose and see how the pipeline catches it
5. Add a new step of your own
