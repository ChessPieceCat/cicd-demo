# CI/CD Demo

[![Build Docker Image](https://github.com/ChessPieceCat/cicd-demo/actions/workflows/build.yml/badge.svg)](https://github.com/ChessPieceCat/cicd-demo/actions/workflows/build.yml)
[![Deploy to Home Server](https://github.com/ChessPieceCat/cicd-demo/actions/workflows/deploy.yml/badge.svg)](https://github.com/ChessPieceCat/cicd-demo/actions/workflows/deploy.yml)
![Ubuntu](https://img.shields.io/badge/Ubuntu-26.04_LTS-E95420?logo=ubuntu\&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker\&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=github-actions\&logoColor=white)

A demonstration of a complete Docker-based Continuous Integration and Continuous Deployment (CI/CD) pipeline using GitHub Actions, Docker, GitHub Container Registry (GHCR), and a self-hosted Ubuntu deployment server.

The goal of this project is to demonstrate a modern deployment workflow that automatically builds, publishes, and deploys a containerized application whenever changes are merged into a protected `main` branch.

<p align="center">
  <img src="diagrams/cicd-overview.drawio.svg" alt="CI/CD Pipeline Overview" width="650">
</p>

---

## Overview

This project focuses on building a reliable software delivery pipeline rather than a complex application. It demonstrates a complete CI/CD workflow that can be reused for future projects while showcasing modern DevOps practices.

The pipeline automatically:

* Builds Docker images using GitHub Actions
* Publishes images to GitHub Container Registry (GHCR)
* Deploys to a self-hosted Ubuntu server
* Verifies successful deployment with health checks

---

## Features

* Automated Docker image builds using GitHub Actions
* Docker Buildx with build layer caching
* Automatic publishing to GitHub Container Registry (GHCR)
* Immutable Docker image tagging using Git commit SHAs
* Self-hosted deployment runner
* Automated deployment verification
* Protected `main` branch with Pull Request workflow
* Docker Compose based deployments

---

## CI/CD Workflow

1. Development is performed on a feature branch.
2. A Pull Request is opened against the protected `main` branch.
3. GitHub Actions builds the Docker image.
4. The image is tagged with both `latest` and the Git commit SHA.
5. The image is pushed to GitHub Container Registry.
6. After the Pull Request is merged, the deployment workflow executes on a self-hosted GitHub Actions runner.
7. Docker Compose pulls the newest image and recreates the container.
8. A health check verifies that the deployment completed successfully.

---

## Architecture

The pipeline intentionally separates **continuous integration** from **continuous deployment**.

GitHub-hosted runners perform all build operations and publish Docker images to GitHub Container Registry. A self-hosted GitHub Actions runner located on the deployment server is responsible only for deployment. Once a successful build is detected on the protected `main` branch, the server automatically pulls the newest container image, recreates the container with Docker Compose, and verifies that the application is healthy.

This design keeps builds isolated from the deployment environment while allowing deployments to occur entirely within the private network.

---

## Technology Stack

| Category           | Technologies                      |
| ------------------ | --------------------------------- |
| Source Control     | Git, GitHub                       |
| CI/CD              | GitHub Actions                    |
| Containerization   | Docker, Docker Compose            |
| Container Registry | GitHub Container Registry (GHCR)  |
| Build System       | Docker Buildx                     |
| Deployment         | Self-hosted GitHub Actions Runner |
| Operating System   | Ubuntu Server 26.04 LTS           |

---

## Repository Structure

```text
.
├── .github/
│   └── workflows/
│       ├── build.yml
│       └── deploy.yml
├── diagrams/
│   ├── cicd-overview.drawio
│   └── cicd-overview.drawio.svg
├── Dockerfile
├── compose.yaml
├── index.html
└── README.md
```

---

## Why I Built This

I created this project to gain practical experience designing and implementing a complete deployment pipeline rather than simply learning individual tools in isolation.

Throughout development I gained hands-on experience with:

* GitHub Actions workflow design
* Docker image creation and optimization
* GitHub Container Registry
* Self-hosted GitHub Actions runners
* Branch protection and Pull Request workflows
* Immutable Docker image tagging
* Automated deployment verification
* Docker Compose deployments

The resulting pipeline is intended to serve as a reusable deployment template for future projects.

---

## Lessons Learned

Some of the most valuable experience came from troubleshooting real deployment issues rather than simply following tutorials.

Key takeaways include:

* Understanding the separation between CI and CD responsibilities.
* Configuring GitHub Rulesets and protected branches for a practical development workflow.
* Working with Docker Buildx and build caching.
* Debugging self-hosted GitHub Actions runners.
* Using immutable Docker image tags to improve deployment traceability.
* Designing deployments that are automated, repeatable, and verifiable.

---

## Future Improvements

Potential future enhancements include:

* Automated rollback if deployment verification fails
* Integration and end-to-end testing before deployment
* Semantic versioning with GitHub Releases
* Deployment notifications
* Multi-environment deployments (development, staging, production)
* Infrastructure as Code integration

---

## License

This project is provided for educational and portfolio purposes.
