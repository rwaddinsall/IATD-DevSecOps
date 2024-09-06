# IATD-DevSecOps

Vulnerable application for DevSecOps Microcredential

The repository was cloned from [https://github.com/erev0s/VAmPI](https://github.com/erev0s/VAmPI)

# CI/CD Pipeline:

# CI-Pipeline.yml

## Python test and build

This GitHub Actions workflow is responsible for running tests, generating code coverage reports, and performing various security scans and checks for a Python project. It consists of the following jobs:

- `test`: This job runs tests using pytest and generates code coverage reports. It installs dependencies, runs the tests, and archives the test results.
- `sonarqube`: This job performs a SonarQube scan for code quality and security analysis. It depends on the `test` job and requires the SonarQube token and URL to be configured as secrets.
- `dast`: This job performs Dynamic Application Security Testing (DAST) using ZAP (Zed Attack Proxy). It depends on the `test` job and deploys a Docker container app for testing. It scans the app using ZAP and uploads the scan report.
- `image-scan`: This job scans the Docker image using Anchore for vulnerabilities. It depends on the `test` job and uploads the scan report.
- `security_gate`: This job downloads the SonarQube, ZAP, and image scan reports, and checks for any high severity vulnerabilities. If any vulnerabilities are found, the job fails.
- `build`: This job builds and pushes the Docker image to Docker Hub. It depends on the `security_gate` job and signs the image using Cosign.
- `submit_reports`: This job uploads the SonarQube, ZAP, and image scan reports to an Azure API endpoint.

The workflow is triggered on every push to the repository. Each job runs on an Ubuntu latest runner.
name: Python test and build

# CD-Pipeline.yml

## Deploy Container App

This GitHub Actions workflow is designed to deploy a container application to Azure. It includes steps for verifying the Docker image signature, logging into Azure, deploying the container app, and submitting deployment results. It consists of the following jobs:

- `deploy`: This job installs Cosign, verifies the Docker image signature, logs into Azure, and deploys the container app.
- `submit_results`: This job logs into Azure, runs an Azure CLI script, and uploads the deployment results.

The workflow is manually triggered using the `workflow_dispatch` event. Each job runs on an Ubuntu latest runner.
