**Secure CI/CD AppSec Pipeline**

Overview

This project demonstrates an automated AppSec/DevSecOps pipeline built using OWASP Juice Shop and GitHub Actions.

The goal was to integrate multiple security tools into a CI/CD workflow and automate security testing against a deployed application.

⸻

Technologies Used

* GitHub Actions
* OWASP Juice Shop
* Semgrep
* Gitleaks
* Trivy
* OWASP ZAP
* Docker
* WSL Ubuntu
* Node.js
* Render

⸻

Security Pipeline

The pipeline performs:

* Static Application Security Testing (SAST)
* Secret Scanning
* Dependency Vulnerability Scanning
* Dynamic Application Security Testing (DAST)
* Automated CI/CD workflow execution

⸻

Security Tools

Semgrep

Used for SAST scanning and insecure code pattern detection.

Gitleaks

Used for secret scanning and credential detection.

Trivy

Used for dependency vulnerability scanning.

OWASP ZAP

Used for automated DAST scanning against the deployed Juice Shop application.

⸻

Deployment

The application was deployed publicly using Render.

⸻

Key Learning Outcomes

* GitHub Actions workflow automation
* CI/CD pipeline design
* AppSec tooling integration
* DAST vs SAST concepts
* Cloud-hosted application scanning
* Debugging CI/CD pipelines
* Security automation practices

⸻

Future Improvements

* AWS deployment
* Kubernetes integration
* Container security hardening
* Security gates for HIGH/CRITICAL findings
* SARIF reporting integration
