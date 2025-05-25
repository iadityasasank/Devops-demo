# DevOps Demo Project

![GitHub Actions Workflow Status](https://github.com/iadityasasank/Devops-demo/actions/workflows/docker-build.yml/badge.svg)

This repository demonstrates a basic DevOps pipeline implementation using GitHub Actions, featuring automated testing and Docker container builds.

## Features

- Automated testing with Python
- Docker container build and push to GitHub Container Registry
- Continuous Integration/Continuous Deployment (CI/CD) pipeline
- Automated dependency management

## CI/CD Pipeline

The pipeline consists of two main jobs:

1. **Test Job**

   - Runs on Ubuntu latest
   - Sets up Python 3.9
   - Installs dependencies
   - Executes test suite using `make test`

2. **Build Job**
   - Builds Docker container
   - Pushes to GitHub Container Registry (ghcr.io)
   - Tags images with latest version

## Getting Started

### Prerequisites

- Python 3.9
- Docker
- Make

### Local Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/iadityasasank/Devops-demo.git
   cd Devops-demo
   ```

2. Install dependencies:

   ```bash
   make install  # If you have a Makefile
   ```

3. Run tests locally:
   ```bash
   make test
   ```

### Docker

Pull the latest image:

```bash
docker pull ghcr.io/iadityasasank/devops-demo:latest
```

Run the container:

```bash
docker run ghcr.io/iadityasasank/devops-demo:latest
```

## GitHub Actions Workflow

The workflow is triggered on:

- Push to master/main branch
- Pull requests to master/main branch

### Workflow Steps:

1. **Test Stage**

   - Checkout code
   - Setup Python environment
   - Install dependencies
   - Run test suite

2. **Build Stage**
   - Authenticate with GitHub Container Registry
   - Build Docker image
   - Push to container registry

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

# Python Flask - Demo Web Application

This is a simple Python Flask web application. The app provides system information and a realtime monitoring screen with dials showing CPU, memory, IO and process information.

The app has been designed with cloud native demos & containers in mind, in order to provide a real working application for deployment, something more than "hello-world" but with the minimum of pre-reqs. It is not intended as a complete example of a fully functioning architecture or complex software design.

Typical uses would be deployment to Kubernetes, demos of Docker, CI/CD (build pipelines are provided), deployment to cloud (Azure) monitoring, auto-scaling

## Screenshot

![screen](https://user-images.githubusercontent.com/14982936/30533171-db17fccc-9c4f-11e7-8862-eb8c148fedea.png)

# Status

![](https://img.shields.io/github/last-commit/benc-uk/python-demoapp) ![](https://img.shields.io/github/release-date/benc-uk/python-demoapp) ![](https://img.shields.io/github/v/release/benc-uk/python-demoapp) ![](https://img.shields.io/github/commit-activity/y/benc-uk/python-demoapp)

Live instances:

[![](https://img.shields.io/website?label=Hosted%3A%20Azure%20App%20Service&up_message=online&url=https%3A%2F%2Fpython-demoapp.azurewebsites.net%2F)](https://python-demoapp.azurewebsites.net/)  
[![](https://img.shields.io/website?label=Hosted%3A%20Kubernetes&up_message=online&url=https%3A%2F%2Fpython-demoapp.kube.benco.io%2F)](https://python-demoapp.kube.benco.io/)

## Building & Running Locally

### Pre-reqs

- Be using Linux, WSL or MacOS, with bash, make etc
- [Python 3.8+](https://www.python.org/downloads/) - for running locally, linting, running tests etc
- [Docker](https://docs.docker.com/get-docker/) - for running as a container, or image build and push
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux) - for deployment to Azure

Clone the project to any directory where you do development work

```
git clone https://github.com/benc-uk/python-demoapp.git
```

### Makefile

A standard GNU Make file is provided to help with running and building locally.

```text
help                 💬 This help message
lint                 🔎 Lint & format, will not fix but sets exit code on error
lint-fix             📜 Lint & format, will try to fix errors and modify code
image                🔨 Build container image from Dockerfile
push                 📤 Push container image to registry
run                  🏃 Run the server locally using Python & Flask
deploy               🚀 Deploy to Azure Web App
undeploy             💀 Remove from Azure
test                 🎯 Unit tests for Flask app
test-report          🎯 Unit tests for Flask app (with report output)
test-api             🚦 Run integration API tests, server must be running
clean                🧹 Clean up project
```

Make file variables and default values, pass these in when calling `make`, e.g. `make image IMAGE_REPO=blah/foo`

| Makefile Variable | Default                |
| ----------------- | ---------------------- |
| IMAGE_REG         | ghcr<span>.</span>io   |
| IMAGE_REPO        | benc-uk/python-demoapp |
| IMAGE_TAG         | latest                 |
| AZURE_RES_GROUP   | temp-demoapps          |
| AZURE_REGION      | uksouth                |
| AZURE_SITE_NAME   | pythonapp-{git-sha}    |

The app runs under Flask and listens on port 5000 by default, this can be changed with the `PORT` environmental variable.

# Containers

Public container image is [available on GitHub Container Registry](https://github.com/users/benc-uk/packages/container/package/python-demoapp)

Run in a container with:

```bash
docker run --rm -it -p 5000:5000 ghcr.io/benc-uk/python-demoapp:latest
```

Should you want to build your own container, use `make image` and the above variables to customise the name & tag.

## Kubernetes

The app can easily be deployed to Kubernetes using Helm, see [deploy/kubernetes/readme.md](deploy/kubernetes/readme.md) for details

# GitHub Actions CI/CD

A working set of CI and CD release GitHub Actions workflows are provided `.github/workflows/`, automated builds are run in GitHub hosted runners

### [GitHub Actions](https://github.com/benc-uk/python-demoapp/actions)

[![](https://img.shields.io/github/workflow/status/benc-uk/python-demoapp/CI%20Build%20App)](https://github.com/benc-uk/python-demoapp/actions?query=workflow%3A%22CI+Build+App%22)

[![](https://img.shields.io/github/workflow/status/benc-uk/python-demoapp/CD%20Release%20-%20AKS?label=release-kubernetes)](https://github.com/benc-uk/python-demoapp/actions?query=workflow%3A%22CD+Release+-+AKS%22)

[![](https://img.shields.io/github/workflow/status/benc-uk/python-demoapp/CD%20Release%20-%20Webapp?label=release-azure)](https://github.com/benc-uk/python-demoapp/actions?query=workflow%3A%22CD+Release+-+Webapp%22)

[![](https://img.shields.io/github/last-commit/benc-uk/python-demoapp)](https://github.com/benc-uk/python-demoapp/commits/master)

## Running in Azure App Service (Linux)

If you want to deploy to an Azure Web App as a container (aka Linux Web App), a Bicep template is provided in the [deploy](deploy/) directory

For a super quick deployment, use `make deploy` which will deploy to a resource group, temp-demoapps and use the git ref to create a unique site name

```bash
make deploy
```

## Running in Azure App Service (Windows)

Just don't, it's awful
