# CI/CD with Docker

## Overview

This project demonstrates how to set up Continuous Integration and Continuous Deployment (CI/CD) using Docker. The setup includes:

- **Creating a Dockerfile**: Define the image with all necessary configurations and dependencies.
- **Setting Up a Self-Hosted Runner**: Configure a GitHub Actions self-hosted runner for executing workflows.
- **Creating a GitHub Workflow**: Develop workflows to automate build, test, and deployment processes.

## Docker Compose Configuration

Below is the configuration for setting up a self-hosted GitHub Actions runner using Docker Compose:

```yaml
version: "3.7"

services:
  runner:
    image: myoung34/github-runner:latest
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      RUNNER_SCOPE: repo
      RUNNER_NAME_PREFIX: myrunner
      LABELS: some-label
      REPO_URL: YOUR_REPO_LINK
      EPHEMERAL: 1
      ACCESS_TOKEN: YOUR_ACCESS_TOKEN
    deploy:
      replicas: 3
      resources:
        limits:
          cpus: '1'
          memory: 1G
        reservations:
          cpus: '0.2'
          memory: 256M
```
## Getting Started

Clone the Repository: Clone this repository to your local machine.

**Configure the Runner**:
- Replace YOUR_REPO_LINK with your GitHub repository URL.
- Replace YOUR_ACCESS_TOKEN with your GitHub access token.
</br>
**Deploy the Stack**:
- Run docker-compose up -d to start the GitHub Actions runner.
