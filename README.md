# IATD-DevSecOps

This repository is a fork from the original VAmPI project, customized to include CI/CD pipelines for automated security scans and deployment.

## GitHub Workflows

### CI Pipeline

The CI pipeline is defined in `.github/workflows/ci-pipeline.yml`. It includes several jobs to ensure code quality, security, and functionality.

#### Test Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Checkout the repository.
2. Set up Python.
3. Install dependencies.
4. Run tests with pytest and generate code coverage reports.
5. Archive code coverage results.

#### SonarQube Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Checkout the repository.
2. Run SonarQube scan for code quality and security analysis.
3. Download and upload SonarQube report.

#### DAST Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Checkout the repository.
2. Set up QEMU and Docker Buildx.
3. Login to Docker Hub.
4. Build and push Docker image.
5. Deploy DAST Container App to Azure.
6. Get deployed DAST app URL.
7. Run ZAP Scan.
8. Upload ZAP report.

#### Image Scan Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Scan Docker image using Anchore.
2. Upload image scan report.

#### Security Gate Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Download SonarQube, ZAP, and image scan reports.
2. Read reports and check for high severity vulnerabilities.
3. Fail the build if any high severity vulnerabilities are found.

#### Build Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Set up QEMU and Docker Buildx.
2. Login to Docker Hub.
3. Build and push Docker image with SBOM and provenance.
4. Install Cosign.
5. Sign the images with GitHub OIDC Token.

#### Submit Reports Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Login to Azure.
2. Upload reports to Azure.

### CD Pipeline

The CD pipeline is defined in `cd-pipeline.yml`. It includes jobs to deploy the application and submit results.

#### Deploy Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Install Cosign.
2. Verify image signature with Cosign.
3. Login to Azure.
4. Deploy Container App to Azure.

#### Submit Results Job

**Runs on:** `ubuntu-latest`

**Steps:**
1. Login to Azure.
2. Upload reports to Azure.

## Usage

To run the application locally, use the following command:

```bash
# Add your command here
```

To run the application using Docker, use:

```bash
# Add your Docker command here
```

## Conclusion

This project demonstrates my skills in DevSecOps and security by implementing secure and automated pipelines using GitHub Actions. It provides a robust and efficient DevSecOps lifecycle, ensuring code quality, security, and functionality.

Feel free to explore the repository and use it for learning and testing purposes. If you have any questions or feedback, please reach out!

**Author:** Rhys Addinsall 2024