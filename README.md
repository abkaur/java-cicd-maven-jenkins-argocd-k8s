# Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD, Helm and Kubernetes

![CI/CD Architecture](./docs/Java-pipeline-architecture.png)



# 🚀 Java Spring Boot CI/CD Pipeline with Jenkins, SonarQube, Docker, Argo CD, and Kubernetes

This repository demonstrates a complete **CI/CD pipeline** for a Java Spring Boot application built with **Maven**.
The pipeline automates building, scanning, containerizing, and deploying the application on a **Kubernetes cluster** using **Argo CD (GitOps)**.

Although this version uses **plain Kubernetes manifests**, it is designed to be easily extendable to **Helm charts** for future scalability and environment-based deployments.

---

## 🧭 Architecture Overview

The CI/CD flow is as follows:

1. **Developer pushes code** → Jenkins is triggered via webhook.
2. **Jenkins pipeline stages:**

   * Checkout source code
   * Build with Maven
   * Run tests and SonarQube analysis
   * Build & push Docker image to Docker Hub
   * Update Kubernetes manifest file (`deployment.yaml`)
3. **Argo CD** detects the change in the manifest repo and auto-syncs the latest image to the Kubernetes cluster.

---

## ▶️ How to Run (High Level)

1. Push a change to `spring-boot-app/` → Jenkins builds, scans, and pushes the image.
2. Jenkins updates `spring-boot-app-manifests/deployment.yaml` with the new image tag.
3. Argo CD auto-syncs and deploys the new version to the cluster.

> For full setup steps, Jenkins plugins, and screenshots, see the documentation in `docs/SETUP.md`.

---

## 🧠 What I Practiced / Learned

* Implemented an **automated CI/CD workflow** integrating Jenkins, SonarQube, Docker, and Argo CD.
* Practiced **GitOps** by automatically updating manifests and syncing deployments.
* Understood **Kubernetes manifests (Deployment & Service)** and how image updates propagate through Argo CD.
* Improved debugging skills for Jenkins pipeline errors, Docker build issues, and Argo CD sync problems.
* Learned the importance of image versioning and repository tagging in production pipelines.

---

## ✅ Tech Stack

Java • Spring Boot • Maven • Jenkins (Pipeline) • SonarQube • Docker • Kubernetes • Argo CD (GitOps)

---

## 📁 Project Structure

```
java-cicd-maven-jenkins-argocd-k8s/
├─ spring-boot-app/             # Source code + Jenkinsfile + Dockerfile + pom.xml
├─ spring-boot-app-manifests/   # Kubernetes manifests (Deployment, Service)
├─ docs/
│   ├─ pipeline-architecture.png
│   ├─ CI-CD-Java-Pipeline-Report.pdf
│   └─ SETUP.md
└─ README.md
```

---

## 🧱 Helm Integration — For Future Enhancement

While this project currently uses **raw Kubernetes manifests**, it can be easily upgraded to use **Helm** for better scalability and environment-specific configurations.

If Helm were to be implemented, the structure would look like this:

```
helm/
└─ spring-boot-app/
   ├─ Chart.yaml                 # Defines the Helm chart and metadata
   ├─ values.yaml                # Central configuration for image tag, replicas, etc.
   └─ templates/
       ├─ deployment.yaml        # Template for Kubernetes deployment
       ├─ service.yaml           # Template for service exposure
```

Helm allows:

* Reusability of templates for multiple environments (dev, staging, prod).
* Parameterized deployment via `values.yaml`.
* Version-controlled chart management for GitOps pipelines.

If integrated, **Jenkins** would update the `values.yaml` file instead of raw YAML manifests, and **Argo CD** would synchronize based on the Helm chart repository.

---

## 📄 Reference Materials

* **Report:** `docs/CI-CD-Java-Pipeline-Report.pdf`
* **Architecture Diagram:** `docs/pipeline-architecture.png`
* **Setup Documentation:** `docs/SETUP.md`

---

💬 *Developed by Abhijot Kaur — demonstrating end-to-end CI/CD automation with Jenkins, Docker, SonarQube, Argo CD, and Kubernetes, with future scalability to Helm-based deployments.*

