# 🚀 Node.js Application CI/CD using Reusable GitHub Actions

## 📌 Overview

This repository demonstrates a **production-grade CI/CD pipeline** using **GitHub Actions reusable workflows**.

Instead of defining pipelines locally, it calls centralized reusable workflows for consistency and scalability.

---

## 🏗️ Architecture

* Caller Repo → triggers pipeline
* Reusable Workflows Repo → executes pipeline logic
* AWS → ECR (image storage) + EKS (deployment)

---

## 📂 Structure

```id="c3d4e5"
.github/workflows/
├── feature-pipeline.yaml
├── dev-nodejs-pipeline.yaml
├── non-prod-pipeline.yaml
```

---

## ⚙️ How It Works

### 🔹 Step 1: Code Push

Pipeline triggers on `push`

### 🔹 Step 2: Call Reusable Workflow

```yaml id="d4e5f6"
uses: org/repo/.github/workflows/dev-nodejs-pipeline.yaml@main
```

---

### 🔹 Step 3: Pipeline Execution

* Install dependencies
* Run unit tests
* Build Docker image
* Scan image using Trivy
* Push to AWS ECR
* Deploy to EKS using Helm

---

## 🐳 Versioning Strategy

* Uses **commit SHA (first 9 chars)** as version
* Example:

```
image: catalogue:1a2b3c4d5
```

---

## 🔁 Commit Status Checks

Each stage updates GitHub commit status:

* UNIT_TESTS
* DOCKER_BUILD
* SECURITY_CHECK
* DEV_DEPLOY

---

## 🔐 Deployment Control

* Pipelines are environment-specific
* No direct uncontrolled production deployment
* Supports validation and approval workflows

---

## ☁️ AWS Integration

* ECR → image storage
* EKS → Kubernetes deployment
* IAM credentials via GitHub secrets

---

## 🚀 Benefits

* Clean separation of pipeline logic
* Reusable and scalable CI/CD
* Secure and automated deployments
* Full traceability using commit-based versioning

---

## 👨‍💻 Author

Pavan – DevOps Engineer
