# 🚀 Azure DevOps CI/CD Pipeline

> **Project Status: 🚧 In Progress**

An end-to-end DevOps project designed to automate application build, testing, containerization, image publishing, and deployment to **Azure Kubernetes Service (AKS)** using **Azure DevOps YAML pipelines**.

The project is being developed step by step with a production-oriented CI/CD approach.

---

## 📌 Project Overview

This project demonstrates an automated CI/CD workflow using:

**Git → Azure DevOps → YAML Pipeline → Docker → Azure Container Registry (ACR) → AKS → Kubernetes**

The objective is to create a reliable deployment pipeline where a code change pushed to the Git repository can automatically move through build, test, containerization, and Kubernetes deployment stages.

### Planned Workflow

```text
Developer
    ↓
Git Repository
    ↓
Azure DevOps YAML Pipeline
    ↓
Build
    ↓
Unit Tests
    ↓
Docker Image Build
    ↓
Azure Container Registry
    ↓
AKS Deployment
    ↓
Kubernetes Pods
    ↓
Application
    ↓
Monitoring
```

---

## 🏗️ Planned Architecture

```text
                         ┌───────────────────┐
                         │    Developer      │
                         │     Git Push      │
                         └─────────┬─────────┘
                                   │
                                   ▼
                         ┌───────────────────┐
                         │   Git Repository  │
                         │   GitHub / Repos   │
                         └─────────┬─────────┘
                                   │
                                   ▼
                         ┌───────────────────┐
                         │   Azure DevOps    │
                         │   YAML Pipeline   │
                         └─────────┬─────────┘
                                   │
                     ┌─────────────┼─────────────┐
                     │             │             │
                     ▼             ▼             ▼
                   Build         Test      Docker Build
                     │             │             │
                     └─────────────┼─────────────┘
                                   ▼
                         ┌───────────────────┐
                         │ Azure Container   │
                         │ Registry (ACR)    │
                         └─────────┬─────────┘
                                   │
                                   ▼
                         ┌───────────────────┐
                         │       AKS         │
                         │    Kubernetes     │
                         └─────────┬─────────┘
                                   │
                     ┌─────────────┼─────────────┐
                     ▼             ▼             ▼
                   Pod 1         Pod 2        Pod N
                     │             │             │
                     └─────────────┼─────────────┘
                                   ▼
                         ┌───────────────────┐
                         │ Kubernetes       │
                         │ Service / LB     │
                         └─────────┬─────────┘
                                   ▼
                              End Users
                                   │
                                   ▼
                         Azure Monitor
```

---

## 🧰 Technologies

| Technology               | Purpose                      |
| ------------------------ | ---------------------------- |
| Azure                    | Cloud infrastructure         |
| Azure DevOps             | CI/CD automation             |
| Git                      | Version control              |
| GitHub / Azure Repos     | Source code management       |
| YAML                     | Pipeline definition          |
| Docker                   | Application containerization |
| Azure Container Registry | Docker image storage         |
| Kubernetes               | Container orchestration      |
| AKS                      | Managed Kubernetes           |
| kubectl                  | Kubernetes administration    |
| Python / Flask           | Sample application           |
| Pytest                   | Unit testing                 |
| Azure Monitor            | Monitoring and observability |

---

## 🎯 Project Objectives

* Automate application build and testing.
* Create Docker images automatically.
* Push container images to Azure Container Registry.
* Deploy applications to Azure Kubernetes Service.
* Manage Kubernetes workloads using YAML manifests.
* Implement rolling deployments.
* Configure application health probes.
* Support deployment verification and rollback.
* Implement secure Azure DevOps service connections.
* Add monitoring and operational visibility.
* Follow DevOps and CI/CD best practices.

---

## 📂 Project Structure

```text
project1-azure-devops/
│
├── app/
│   ├── app.py
│   └── requirements.txt
│
├── tests/
│   └── test_app.py
│
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
│
├── Dockerfile
├── .dockerignore
├── azure-pipelines.yml
└── README.md
```

---

## 🔄 CI/CD Pipeline

The planned pipeline will contain the following stages:

### Stage 1 — Build

* Checkout source code
* Install dependencies
* Build application
* Validate source

### Stage 2 — Test

* Run unit tests
* Validate application health
* Stop pipeline if tests fail

### Stage 3 — Docker

* Build Docker image
* Tag image with pipeline build ID
* Push image to ACR

### Stage 4 — Deploy

* Connect to AKS
* Deploy Kubernetes manifests
* Update container image
* Wait for rollout completion

### Stage 5 — Verify

* Check deployment status
* Check pod status
* Check service status
* Validate application endpoint

### Stage 6 — Monitor

* Collect application/container logs
* Monitor Kubernetes resources
* Configure Azure monitoring and alerts

---

## ☸️ Kubernetes Components

The project will use:

### Deployment

Manages application replicas and rolling updates.

```yaml
replicas: 2
```

### Service

Exposes the application through a Kubernetes service.

Planned service type:

```yaml
type: LoadBalancer
```

### Health Probes

Planned:

* Liveness Probe
* Readiness Probe

These help Kubernetes determine application health and readiness.

---

## 🐳 Docker Strategy

The application will be packaged as a Docker image.

Example image:

```text
acrdevopsproject1.azurecr.io/devops-app:<build-id>
```

Pipeline flow:

```text
Source Code
    ↓
Docker Build
    ↓
Docker Image
    ↓
ACR
    ↓
AKS
```

Versioned image tags will be used for deployment traceability.

---

## ☁️ Azure Resources

Planned Azure resources:

```text
Resource Group
│
├── Azure Container Registry
│
└── Azure Kubernetes Service
```

Example naming:

```text
Resource Group:
rg-devops-project1

ACR:
acrdevopsproject1

AKS:
aks-devops-project1
```

---

## 🔐 Security

Security will be implemented progressively during the project.

Planned practices:

* Azure DevOps service connections
* Secure authentication to Azure resources
* No passwords or secrets committed to Git
* Secret management using Azure-native mechanisms
* Least-privilege access where practical
* Kubernetes RBAC
* Container/image security scanning

---

## 🧪 Testing Strategy

### Application Testing

```bash
pytest
```

### Docker Testing

```bash
docker build
docker run
```

### Kubernetes Testing

```bash
kubectl get pods
kubectl get deployments
kubectl get services
kubectl rollout status deployment/devops-app
```

### Deployment Validation

Verify:

* Pod status
* Replica count
* Service availability
* Application health endpoint
* Deployment rollout status

---

## 🔄 Deployment Strategy

The project is planned to use **rolling updates**.

Example:

```text
Version 1
   ↓
Build
   ↓
Docker Image
   ↓
ACR
   ↓
AKS
   ↓
Version 2
```

Old pods will be replaced progressively rather than stopping the entire application at once.

Rollback will be tested using Kubernetes rollout functionality.

---

## 📈 Monitoring

Planned monitoring capabilities:

* AKS node health
* Pod status
* CPU utilization
* Memory utilization
* Container logs
* Kubernetes events
* Application health
* Deployment status

Target:

```text
AKS
 ↓
Azure Monitor
 ↓
Metrics
 ↓
Logs
 ↓
Alerts
```

---

## 🛠️ Implementation Progress

### Phase 1 — Application

* [ ] Create sample application
* [ ] Add health endpoint
* [ ] Add unit tests
* [ ] Validate application locally

### Phase 2 — Docker

* [ ] Create Dockerfile
* [ ] Create `.dockerignore`
* [ ] Build image
* [ ] Test container locally

### Phase 3 — Azure

* [ ] Create Resource Group
* [ ] Create Azure Container Registry
* [ ] Create AKS cluster
* [ ] Configure ACR → AKS access

### Phase 4 — Kubernetes

* [ ] Create Deployment manifest
* [ ] Create Service manifest
* [ ] Configure replicas
* [ ] Add health probes
* [ ] Perform manual deployment

### Phase 5 — Azure DevOps

* [ ] Create Azure DevOps project
* [ ] Configure repository
* [ ] Create service connections
* [ ] Create YAML pipeline
* [ ] Configure CI
* [ ] Configure CD

### Phase 6 — Validation

* [ ] Test automatic pipeline trigger
* [ ] Verify Docker image in ACR
* [ ] Verify AKS deployment
* [ ] Test rolling update
* [ ] Test rollback

### Phase 7 — Monitoring & Security

* [ ] Configure Azure Monitor
* [ ] Add alerts
* [ ] Improve secret management
* [ ] Add image/security scanning

---

## 🚧 Current Status

**Project Status: In Progress**

Current work is focused on building and validating the project incrementally.

The final implementation will include:

```text
Git
 ↓
Azure DevOps
 ↓
CI Pipeline
 ↓
Docker
 ↓
ACR
 ↓
CD Pipeline
 ↓
AKS
 ↓
Kubernetes
 ↓
Monitoring
```

Features marked as incomplete in the checklist will be added and validated during subsequent development phases.

---

## 📸 Project Evidence

Screenshots and implementation evidence will be added as the project progresses.

Planned evidence:

```text
screenshots/
├── azure-resources.png
├── azure-devops-pipeline.png
├── pipeline-success.png
├── acr-image.png
├── aks-pods.png
├── aks-service.png
├── application-running.png
├── rolling-update.png
└── azure-monitor.png
```

---

## 📚 Key DevOps Concepts Demonstrated

This project is intended to demonstrate practical understanding of:

* Continuous Integration (CI)
* Continuous Delivery / Deployment (CD)
* Azure DevOps YAML pipelines
* Git workflows
* Docker containerization
* Azure Container Registry
* Kubernetes Deployments
* Kubernetes Services
* AKS
* Rolling updates
* Health probes
* Rollback
* Service connections
* Container image versioning
* Monitoring and observability
* DevOps security practices

---

## 👨‍💻 Author

**Rafeek Ahamed M**

DevOps Engineer | Azure Cloud Engineer

---

## ⚠️ Project Disclaimer

This repository represents a hands-on learning and portfolio project.

The implementation is being developed incrementally, and the README will be updated as additional CI/CD, Kubernetes, security, and monitoring components are completed.
