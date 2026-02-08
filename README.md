# CI with GitHub Actions + Jenkins CD

This repository demonstrates how to implement **Continuous Integration (CI)** using **GitHub Actions** for tests, and **Continuous Deployment (CD)** via **Jenkins**, triggered remotely via API (no webhooks required).

## Overview

- Code is pushed to GitHub.
- GitHub Actions runs tests automatically.
- If tests succeed, a **Jenkins build is triggered via a remote API call** (`curl`) to start deployment.
- Jenkins builds the Docker image, stops old container, and runs the new container on VPS.
- Secrets (like environment variables) are managed securely Sever.

## Steps

1. **Create a Jenkins job**
   - Pipeline type
   - Connect to Git repository
   - Enable Trigger type "Trigger builds remotely"

2. **Add Jenkinsfile**
   - Build Docker image
   - Stop old container
   - Run new container
   - Inject environment variables from server file (ex: home/docker/api/.env)

3. **Deployment**
   - Run container on VPS with specified port

## Notes

- Ensure VPS has Docker installed
- Use `.env` files securely
