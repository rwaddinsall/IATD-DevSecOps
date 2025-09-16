# IATD-DevSecOps

![CI Status](https://github.com/rwaddinsall/IATD-DevSecOps/actions/workflows/ci-pipeline.yml/badge.svg)
![Security Gate](https://img.shields.io/badge/security--gate-passing-green)
![License](https://img.shields.io/github/license/rwaddinsall/IATD-DevSecOps)

## Overview

DevSecOps pipeline implementation built on VAmPI (Vulnerable API). Demonstrates automated security testing, container signing, and cloud deployment. Part of IAT NSW DevSecOps course.

## Technical Stack

**Security**: SonarQube, OWASP ZAP, Anchore, Cosign  
**Platform**: GitHub Actions, Azure Container Apps, Docker  
**Languages**: Python, YAML, Bash

## Pipeline Architecture

### CI Pipeline (`ci-pipeline.yml`)
- **SAST**: SonarQube static analysis
- **DAST**: OWASP ZAP dynamic scanning  
- **Container Scan**: Anchore vulnerability assessment
- **Security Gate**: Fail on high-severity findings
- **Build**: Multi-stage Docker with SBOM
- **Sign**: Cosign image signing with GitHub OIDC

### CD Pipeline (`cd-pipeline.yml`)
- **Verify**: Cosign signature validation
- **Deploy**: Azure Container Apps
- **Report**: Centralized security artifacts

## Security Controls

| Control | Tool | Coverage |
|---------|------|----------|
| SAST | SonarQube | Code quality + vulnerabilities |
| DAST | OWASP ZAP | Runtime API testing |
| SCA | Anchore | Container vulnerabilities |
| Supply Chain | Cosign | Image signing + SBOM |

## Project Structure

```
├── .github/workflows/
│   ├── ci-pipeline.yml    # Security testing pipeline
│   └── cd-pipeline.yml    # Deployment pipeline
├── app/                   # VAmPI application code
└── Dockerfile            # Multi-stage container build
```

## Implementation Details

**Security Gate Logic**: Parses JSON reports, fails build on CVSS >= 7.0  
**Image Signing**: Keyless signing with GitHub OIDC tokens  
**SBOM Generation**: Docker buildx attestation with provenance  
**Report Storage**: Azure Blob with workflow artifacts



## Key Features

- **Automated Security Gate**: Build fails on CVSS >= 7.0 vulnerabilities
- **Multi-layer Scanning**: SAST, DAST, and container vulnerability detection
- **Supply Chain Security**: SBOM generation and cryptographic image signing
- **Cloud Deployment**: Serverless container deployment to Azure

---

**Rhys Addinsall** | IAT NSW DevSecOps Course | 2024
