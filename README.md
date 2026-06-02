**Secure CI/CD DevSecOps Pipeline for OWASP Juice Shop**

## Overview
This project demonstrates the design and implementation of a secure DevSecOps pipeline using OWASP Juice Shop, a deliberately vulnerable web application, as the target workload. The objective was to integrate security throughout the software development lifecycle by automating code analysis, secret detection, vulnerability assessment, container security, Kubernetes security, and runtime threat monitoring.

The project implements a complete CI/CD workflow using GitHub Actions and incorporates multiple security tools to identify and mitigate risks at different stages of the pipeline. Static Application Security Testing (SAST) is performed using Semgrep, secret detection is handled by Gitleaks, container and dependency vulnerabilities are analyzed using Trivy, and Dynamic Application Security Testing (DAST) is conducted using OWASP ZAP. These controls help identify security issues before and after deployment.

To demonstrate modern cloud-native deployment practices, the application was containerized using Docker and deployed both through Render and a local Kubernetes environment using Minikube. Additional Kubernetes security controls were implemented, including namespace isolation, Network Policies, Role-Based Access Control (RBAC), Kubernetes Secrets, and CIS Benchmark assessments using kube-bench.

The project also includes runtime security monitoring using Falco, which detects suspicious activity within running containers. During testing, Falco successfully generated alerts for container shell execution events, demonstrating real-time threat detection capabilities. This project showcases a practical end-to-end DevSecOps implementation that combines secure development, automated security testing, container security, Kubernetes hardening, and runtime monitoring in a single environment.

## Architecture Diagram
![alt text](<WhatsApp Image 2026-05-31 at 3.29.14 PM.jpeg>)

## Technologies Used
Application

* OWASP Juice Shop
* Node.js

Version Control & CI/CD

* Git
* GitHub
* GitHub Actions

Static Application Security Testing (SAST)

* Semgrep

Secrets Detection

* Gitleaks

Container & Dependency Security

* Trivy

Dynamic Application Security Testing (DAST)

* OWASP ZAP

Containerization

* Docker
* Docker Desktop

Container Registry

* Docker Image Management

Kubernetes & Orchestration

* Kubernetes
* Minikube
* kubectl

Kubernetes Security

* kube-bench
* Network Policies
* RBAC (Role-Based Access Control)
* Kubernetes Secrets
* Namespace Isolation

Runtime Security Monitoring

* Falco

Deployment Platform

* Render

Development Environment

* Visual Studio Code
* Ubuntu (WSL2)

Configuration & Infrastructure

* YAML
* Kubernetes Manifests
* Dockerfile

## Security Tools Implemented

Semgrep (Static Application Security Testing - SAST)

Semgrep was integrated into the CI/CD pipeline to perform Static Application Security Testing (SAST). It analyzes source code without executing the application and helps identify insecure coding patterns, potential vulnerabilities, and security misconfigurations early in the development lifecycle. This allows security issues to be detected before deployment.

Purpose:

* Detect insecure coding practices
* Identify common vulnerability patterns
* Shift security testing left in the SDLC

⸻

Gitleaks (Secrets Detection)

Gitleaks was used to scan the repository for accidentally exposed secrets such as API keys, passwords, tokens, and credentials. Secret scanning was integrated into the CI/CD pipeline to prevent sensitive information from being committed to source control.

Purpose:

* Detect exposed secrets
* Prevent credential leakage
* Improve repository security

⸻

Trivy (Container & Dependency Security)

Trivy was used to scan application dependencies and Docker container images for known vulnerabilities. The tool identifies CVEs (Common Vulnerabilities and Exposures) in operating system packages and application libraries, enabling remediation before deployment.

Purpose:

* Detect vulnerable dependencies
* Scan Docker images
* Identify CVEs and security risks

⸻

OWASP ZAP (Dynamic Application Security Testing - DAST)

OWASP ZAP was integrated to perform Dynamic Application Security Testing (DAST) against the running application. Unlike static analysis, ZAP tests the deployed application and identifies vulnerabilities such as security misconfigurations, missing security headers, and other runtime issues.

Purpose:

* Assess application security during runtime
* Identify web application vulnerabilities
* Validate deployed application security

⸻

kube-bench (Kubernetes Security Benchmarking)

kube-bench was used to assess the Kubernetes environment against the CIS Kubernetes Benchmark. The tool evaluates cluster configurations and provides recommendations for hardening Kubernetes components and improving security posture.

Purpose:

* Perform Kubernetes security assessments
* Validate CIS Benchmark compliance
* Identify cluster hardening opportunities

Key Findings Implemented:

* Namespace isolation
* Network Policies
* RBAC controls
* Security hardening recommendations

⸻

Falco (Runtime Security Monitoring)

Falco was deployed to provide runtime security monitoring within the Kubernetes environment. It continuously monitors system calls and container activity to detect suspicious behavior. During testing, Falco successfully detected shell execution inside a running container, demonstrating its ability to identify potentially malicious activity in real time.

Purpose:

* Monitor runtime container activity
* Detect suspicious behavior and threats
* Provide real-time security alerts

Demonstrated Detection:

* Shell spawned inside a container
* Runtime activity monitoring
* Real-time alert generation

## Containerization
The OWASP Juice Shop application was containerized using Docker to ensure consistent deployment across different environments. Containerization packages the application along with its dependencies, configuration, and runtime requirements into a portable image that can be deployed reliably on any system supporting Docker.

A custom Docker image was built using a Dockerfile and tested locally using Docker Desktop before being integrated into the CI/CD pipeline and Kubernetes environment. The containerized application was also scanned using Trivy to identify vulnerabilities within both application dependencies and the container image itself.

Implementation

Dockerfile

A Dockerfile was created to define the application build process, including:

* Base image selection
* Application dependency installation
* Application startup configuration
* Port exposure for application access

Docker Image Build

The application image was built locally using Docker:

docker build -t juice-shop-appsec:latest

Container Execution

The containerized application was tested locally before deployment:

docker run -d -p 3000:3000 juice-shop-appsec:latest

Security Validation

Container security was validated using Trivy vulnerability scanning to identify:

* Vulnerable operating system packages
* Outdated libraries and dependencies
* Known CVEs (Common Vulnerabilities and Exposures)

Benefits of Containerization

* Consistent deployment across environments
* Improved application portability
* Simplified dependency management
* Faster deployment and rollback capabilities
* Integration with Kubernetes orchestration
* Enhanced security through container scanning and monitoring

Containerization served as the foundation for subsequent Kubernetes deployment, security hardening, and runtime monitoring activities performed in this project.

## Kubernetes Deployment

The containerized OWASP Juice Shop application was deployed to a local Kubernetes cluster using Minikube. Kubernetes was used to automate container orchestration, service exposure, workload management, and security control implementation. This deployment provided hands-on experience with cloud-native application management and Kubernetes security best practices.

Kubernetes Components Implemented

Deployment

A Kubernetes Deployment resource was created to manage the application lifecycle. The deployment ensures that the desired number of application replicas are running and automatically recreates failed containers when necessary.

Key Features:

* Automated pod management
* Self-healing capabilities
* Replica management
* Rolling updates and restarts

Service

A Kubernetes Service was configured to expose the application and enable network access to the deployed pods. The service provides a stable endpoint for communication regardless of pod restarts or recreation.

Benefits:

* Stable networking
* Service discovery
* Traffic routing to application pods

Namespace Isolation

A dedicated namespace was created for the application to provide logical separation from system workloads and improve security management.

Benefits:

* Resource isolation
* Improved organization
* Simplified security policy enforcement

Network Policies

Network Policies were implemented to control network communication between workloads within the cluster. This follows the principle of least privilege by restricting unnecessary traffic between Kubernetes resources.

Benefits:

* Reduced attack surface
* Improved network segmentation
* Enhanced cluster security

Role-Based Access Control (RBAC)

RBAC was implemented using ServiceAccounts, Roles, and RoleBindings to enforce least-privilege access controls within the Kubernetes environment.

Implemented Components:

* ServiceAccount
* Role
* RoleBinding

Benefits:

* Fine-grained access control
* Reduced privilege exposure
* Improved security governance

Kubernetes Secrets

Sensitive configuration values were stored using Kubernetes Secrets and securely injected into application workloads. This prevents sensitive information from being hardcoded within source code or deployment manifests.

Benefits:

* Secure configuration management
* Reduced credential exposure
* Separation of secrets from application code

Security Assessment

The Kubernetes environment was evaluated using kube-bench, which performs CIS Kubernetes Benchmark assessments. The findings were used to identify security hardening opportunities and implement improvements such as namespace isolation, network policies, RBAC, and secrets management.

Runtime Security Monitoring

Falco was deployed within the Kubernetes cluster to provide runtime threat detection and monitoring. During testing, Falco successfully detected shell execution inside a running container, demonstrating the ability to identify potentially suspicious runtime activity in real time.

Outcomes

Through this deployment, the project demonstrates container orchestration, Kubernetes security hardening, workload isolation, access control implementation, secure secret management, and runtime security monitoring within a cloud-native environment.

### Secrets Management
Managing sensitive information securely is a critical component of modern DevSecOps practices. Hardcoding credentials, API keys, passwords, or tokens within source code can lead to accidental exposure through source control systems, logs, or deployment artifacts.

In this project, Kubernetes Secrets were used to securely store sensitive configuration values and inject them into application workloads at runtime. This approach separates secrets from application code and deployment manifests, reducing the risk of credential leakage.

Implementation

A Kubernetes Secret was created to store sensitive application data:

kubectl create secret generic app-secret \
  --from-literal=API_KEY=test123 \
  -n juice-shop

The secret was then referenced within the Kubernetes Deployment manifest and injected into the application container using environment variables.

Secret Injection

env:
  - name: API_KEY
    valueFrom:
      secretKeyRef:
        name: app-secret
        key: API_KEY

This allowed the application to access sensitive configuration values without embedding them directly into source code or container images.

Security Benefits

* Separation of secrets from application code
* Reduced risk of credential exposure
* Improved configuration management
* Simplified secret rotation and updates
* Alignment with Kubernetes security best practices

Future Enhancements

While Kubernetes Secrets were used in this project, production environments typically integrate dedicated secret management solutions such as:

* AWS Secrets Manager
* HashiCorp Vault
* Azure Key Vault
* Google Secret Manager

These solutions provide additional capabilities including encryption, secret rotation, auditing, and centralized secret management.

Key Learning Outcome

This implementation demonstrated how sensitive configuration values can be securely managed and consumed by containerized applications without exposing credentials in source code repositories or deployment artifacts.

## Security Findings
This project incorporated multiple security assessment tools across the software development lifecycle to identify vulnerabilities, security misconfigurations, exposed secrets, container risks, Kubernetes hardening opportunities, and runtime threats. The findings below summarize the results of the implemented security controls and the remediation measures applied during the project.

⸻

Static Application Security Testing (SAST) – Semgrep

Semgrep was integrated into the CI/CD pipeline to perform automated source code analysis. The tool was used to identify insecure coding patterns, potential vulnerabilities, and security misconfigurations before deployment.

Key Outcomes

* Automated security scanning during code changes
* Early identification of potential security weaknesses
* Integration of security testing into the development workflow

<img width="959" height="478" alt="46" src="https://github.com/user-attachments/assets/bc2c4964-99af-49bd-8882-4b88bde4dc65" />


⸻

Secrets Detection – Gitleaks

Gitleaks was used to scan the repository for accidentally exposed secrets such as API keys, tokens, credentials, and sensitive configuration values.

Key Outcomes

* Repository scanned for exposed secrets
* Validation that sensitive information was not committed to source control
* Improved repository security posture

Screenshot

⸻

Container Vulnerability Assessment – Trivy

Trivy was used to assess application dependencies and Docker container images for known vulnerabilities. The scan identified vulnerabilities across operating system packages and application libraries.

Key Findings

* Total Vulnerabilities Detected: 2592
* Critical Vulnerabilities: 25
* High Severity Vulnerabilities: 268
* Medium Severity Vulnerabilities: 1213
* Low Severity Vulnerabilities: 1069

Security Impact

The assessment provided visibility into dependency and container image risks, enabling prioritization of remediation efforts and demonstrating the importance of vulnerability management within containerized environments.

Screenshot

⸻

Dynamic Application Security Testing (DAST) – OWASP ZAP

OWASP ZAP was used to evaluate the running application from an attacker’s perspective. Dynamic testing helped identify potential security weaknesses that may not be visible through static analysis alone.

Key Outcomes

* Runtime application security assessment
* Validation of deployed application security controls
* Identification of potential web application security issues

Screenshot

⸻

Kubernetes Security Assessment – kube-bench

kube-bench was used to evaluate the Kubernetes environment against CIS Kubernetes Benchmark recommendations. The assessment identified several hardening opportunities and security best practices.

Key Findings

* Recommendations for namespace isolation
* Recommendations for network segmentation
* Recommendations for RBAC implementation
* Recommendations for secure secrets management
* Recommendations for workload hardening

Remediation Actions Implemented

* Created a dedicated application namespace
* Implemented Kubernetes Network Policies
* Configured RBAC using ServiceAccounts, Roles, and RoleBindings
* Implemented Kubernetes Secrets for secure configuration management
* Added runtime security monitoring using Falco

Security Impact

The assessment helped improve the security posture of the Kubernetes environment through the implementation of multiple defense-in-depth controls.

Screenshot

⸻

Runtime Threat Detection – Falco

Falco was deployed within the Kubernetes cluster to provide runtime security monitoring. During testing, Falco successfully detected shell execution activity inside a running container.

Detection Demonstrated

* Shell spawned inside a container
* Runtime process monitoring
* Real-time security alert generation

Security Impact

This validated the effectiveness of runtime threat detection and demonstrated the ability to identify potentially suspicious activity occurring within containerized workloads.

Screenshot

⸻

Kubernetes Deployment Validation

The application was successfully deployed to Kubernetes using Minikube and validated using Kubernetes services, deployments, namespaces, and security controls.

Implemented Controls

* Namespace Isolation
* Network Policies
* RBAC
* Kubernetes Secrets
* Runtime Monitoring with Falco

Screenshot

⸻

Overall Security Improvements

The project successfully implemented security controls across multiple layers of the software development lifecycle:

* Source Code Security (Semgrep)
* Secret Detection (Gitleaks)
* Dependency and Container Security (Trivy)
* Dynamic Application Security Testing (OWASP ZAP)
* Kubernetes Security Benchmarking (kube-bench)
* Runtime Threat Detection (Falco)
* Access Control (RBAC)
* Network Segmentation (Network Policies)
* Secure Configuration Management (Kubernetes Secrets)

This layered approach demonstrates how DevSecOps practices can be integrated into modern cloud-native application deployments to improve overall security posture and reduce operational risk.
## Screenshots

## Lessons Learned

## Future Enhancements
## Author

Shravasti Borkar
Application Security Engineer / Pentester

