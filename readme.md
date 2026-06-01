# 🚀 Employee Management System — DevOps CI/CD Pipeline

![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-success)
![Docker](https://img.shields.io/badge/Docker-Hub%20Deployed-blue)
![SonarCloud](https://img.shields.io/badge/Code%20Quality-SonarCloud-orange)
![Slack](https://img.shields.io/badge/Notifications-Slack-purple)
![Java](https://img.shields.io/badge/Java-17-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.14-green)
![Build](https://img.shields.io/badge/Build-Passing-brightgreen)

---

## 📌 Project Overview

This project demonstrates a **production-grade DevOps CI/CD pipeline** for a Java Spring Boot web application. As a DevOps Engineer, I designed and implemented the complete pipeline infrastructure including automated builds, testing, code quality analysis, containerization, and real-time notifications.

---

## 🏗️ Infrastructure Architecture

```
Developer pushes code
        ↓
GitHub Repository (Source Control)
        ↓
GitHub Actions (CI/CD Orchestration)
        ↓
    ┌───────────────────────────────┐
    │        Pipeline Stages        │
    │  1. Checkout Code             │
    │  2. Setup Java 17             │
    │  3. Build (Maven) - 21s       │
    │  4. Test (JUnit + H2) - 8s    │
    │  5. Code Quality (Sonar) - 31s│
    │  6. Login to Docker Hub - 0s  │
    │  7. Build & Push Docker Image │
    └───────────────────────────────┘
        ↓
SonarCloud (Code Quality Gate)
        ↓
Docker Hub (Image Repository)
        ↓
Slack Notification (Team Alert)
```

---

## 🛠️ DevOps Tools & Technologies

| Tool | Purpose | Details |
|---|---|---|
| **GitHub** | Source Control & Pipeline Trigger | Repo hosting, branch protection |
| **GitHub Actions** | CI/CD Orchestration | Automated pipeline on push/PR |
| **SonarCloud** | Code Quality & Security | Bugs, vulnerabilities, code smells |
| **Docker** | Containerization | Multi-stage build, 112.42 MB image |
| **Docker Hub** | Image Registry | laxmir22095/employee-management-cicd |
| **Slack** | Notifications | Real-time build success/failure alerts |
| **Maven** | Build Tool | Dependency management, packaging |
| **H2 Database** | Test Database | In-memory DB for pipeline testing |
| **MySQL** | Production Database | Local development database |

---

## ✅ Pipeline Results (Live)

### GitHub Actions — Build Success:

```
✅ Set up job           2s
✅ Checkout code        1s
✅ Set up Java 17       0s
✅ Build with Maven    21s
✅ Run Tests            8s
✅ SonarCloud Analysis 31s
✅ Login to Docker Hub  0s
✅ Build Docker Image
✅ Push to Docker Hub
✅ Notify Slack

Total Time: 1m 42s ✅
```

> 📸 **GitHub Actions Pipeline — All Steps Passed**
> Pipeline run: `Trigger pipeline after Docker token fix #13`
> Status: ✅ **succeeded 9 minutes ago in 1m 42s**

---

### Docker Hub — Image Deployed:

```
Image:     laxmir22095/employee-management-cicd:latest
Size:      112.42 MB
OS/ARCH:   linux/amd64
Type:      Image
Last Push: 7 minutes ago
```

> 📸 **Docker Hub — Image Successfully Pushed**
> Image layers visible with Java environment configured

---

### SonarCloud — Code Quality Analysis:

```
Project:        employee-management-Java-webapp-cicd-project
Lines of Code:  219
Last Analysis:  6/1/2026, 7:54 PM
HTML, XML analyzed ✅

Security:        B - 2 issues
Reliability:     C - 6 issues
Maintainability: A - 0 issues
Hotspots:        E - 0.0% reviewed
Duplications:    0.0% ✅
```

> 📸 **SonarCloud — Code Quality Report**
> Quality Gate: Failed (1 condition) — Issues assigned to developer for fixing

---

### Slack Notifications — Real-time Alerts:

```
CicdBot  1:19 PM
BUILD SUCCESS: employee-management-cicd pipeline passed!

CicdBot  1:38 PM
❌ BUILD FAILED: employee-management-cicd pipeline failed!

CicdBot  7:55 PM
BUILD SUCCESS: employee-management-cicd pushed to Docker Hub!
```

> 📸 **Slack Channel #all-cicd-pipeline — Notifications Received**
> All build results (success and failures) visible in real-time

---

## ⚙️ CI/CD Pipeline Design

### Pipeline File: `.github/workflows/ci-cd.yml`

### Trigger Strategy:
```yaml
on:
  push:
    branches: [ main ]      # Triggers on every push to main
  pull_request:
    branches: [ main ]      # Triggers on every PR to main
```

### Complete Pipeline:

```yaml
name: Employee Management CI/CD

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - Checkout code
      - Set up Java 17 (Eclipse Temurin)
      - Build with Maven (mvn clean package)
      - Run Tests (JUnit + H2)
      - SonarCloud Analysis
      - Login to Docker Hub
      - Build and Push Docker Image
      - Notify Slack (Success/Failure)
```

---

## 🐳 Docker Strategy

### Multi-Stage Dockerfile:

```dockerfile
# Stage 1: Build Stage
FROM maven:3.9.6-eclipse-temurin-17 AS build
→ Compiles code → Creates .jar file

# Stage 2: Run Stage (Lightweight)
FROM eclipse-temurin:17-jre-alpine
→ Copies .jar → Runs application
```

### Results:
```
Multi Stage Image → 112.42 MB ✅
OS/ARCH          → linux/amd64
Registry         → Docker Hub
```

---

## 🔐 Secrets Management

| Secret Name | Description | Used In |
|---|---|---|
| `SONAR_TOKEN` | SonarCloud auth token | SonarCloud Analysis step |
| `SLACK_WEBHOOK_URL` | Slack incoming webhook | Notification steps |
| `DOCKERHUB_USERNAME` | Docker Hub username | Docker build & push |
| `DOCKER_PASSWORD` | Docker Hub access token | Docker Hub login |

---

## 📊 SonarCloud Quality Report

| Metric | Grade | Issues |
|---|---|---|
| Security | B | 2 |
| Reliability | C | 6 |
| Maintainability | A | 0 |
| Duplications | — | 0.0% |

- **Organization:** laxmi7676
- **Project:** employee-management-Java-webapp-cicd-project
- **Lines of Code:** 219
- **Last Analysis:** 6/1/2026

> Note: Security and Reliability issues are assigned to the development team for fixing as per DevOps workflow.

---

## 💬 Slack Notification Strategy

| Pipeline Result | Slack Message |
|---|---|
| All steps pass | ✅ BUILD SUCCESS: pushed to Docker Hub! |
| Any step fails | ❌ BUILD FAILED: pipeline failed! |

- **Channel:** `#all-cicd-pipeline`
- **Workspace:** CI/CD Pipeline
- **Bot:** CicdBot

---

## 🔧 Local Setup

### Prerequisites:
- Java 17
- Maven
- MySQL 8.0
- Docker (optional)

### Steps:

**1. Clone the repository:**
```bash
git clone https://github.com/Laxmi7676/employee-management-Java-webapp-cicd-project.git
cd employee-management-Java-webapp-cicd-project
```

**2. Create MySQL database:**
```sql
CREATE DATABASE employeedb;
```

**3. Update `application.properties`:**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/employeedb
spring.datasource.username=root
spring.datasource.password=your_password
```

**4. Run the application:**
```bash
mvn spring-boot:run
```

**5. Open browser:**
```
http://localhost:8080
```

---

## 🐳 Run from Docker Hub

```bash
docker pull laxmir22095/employee-management-cicd:latest
docker run -p 8080:8080 laxmir22095/employee-management-cicd:latest
```

---

## 🚨 Pipeline Issues & Fixes

| Error | Cause | Fix Applied |
|---|---|---|
| `Failed to load ApplicationContext` | No MySQL in pipeline | Used H2 in-memory DB |
| `localhost:9000 not reachable` | Wrong SonarCloud URL | Set correct sonarcloud.io URL |
| `Unexpected char in Authorization` | Bad SONAR_TOKEN | Regenerated fresh token |
| `invalid reference format` | Newline in Docker username | Used `tr -d` to trim whitespace |
| `insufficient_scope` | Read-only Docker token | Generated Read & Write token |
| `Dockerfile typo` | eclipse-remurin typo | Fixed to eclipse-temurin |

---

## 📁 Repository Structure

```
employee-management-Java-webapp-cicd-project/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          ← CI/CD Pipeline (DevOps)
├── src/
│   ├── main/
│   │   ├── java/com/example/employee/
│   │   │   ├── controller/    ← REST Controllers
│   │   │   ├── model/         ← Data Models
│   │   │   ├── repository/    ← DB Layer
│   │   │   └── service/       ← Business Logic
│   │   └── resources/
│   │       ├── templates/     ← HTML Pages
│   │       └── application.properties
│   └── test/                  ← Unit Tests (H2)
├── Dockerfile                 ← Containerization
└── pom.xml                    ← Build Config
```

---

## 👩‍💻 DevOps Engineer

**Laxmi Ramanagoudra**
- GitHub: [@Laxmi7676](https://github.com/Laxmi7676)
- Docker Hub: [laxmir22095](https://hub.docker.com/u/laxmir22095)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
