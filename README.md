# CI/CD Pipeline with Jenkins & AWS

A production-grade Continuous Integration and Continuous Deployment (CI/CD) pipeline built using Jenkins, GitHub Actions, Maven, and AWS — designed for automated Java application lifecycle management.

## Project Overview

This project implements a complete CI/CD pipeline that automates the software development lifecycle — from code commit to deployment — with integrated code quality checks, automated testing, and multi-environment AWS deployments.

## Tech Stack

| Tool | Purpose |
|------|---------|
| Jenkins | CI/CD orchestration and pipeline automation |
| GitHub Actions | Workflow triggers and automation |
| Maven | Java build tool — compile, test, package |
| Java | Application language (multi-version support) |
| AWS EC2 | Deployment environment (multi-environment) |
| AWS S3 | Artifact storage |
| SonarQube | Static code analysis and quality gates |
| JUnit | Automated unit testing framework |

## Pipeline Stages

```
Code Commit → GitHub Actions Trigger → Jenkins Pipeline
     │
     ├── 1. Clean          (mvn clean)
     ├── 2. Compile        (mvn compile)
     ├── 3. Test           (mvn test + JUnit)
     ├── 4. Code Analysis  (SonarQube scan)
     ├── 5. Package        (mvn package → .jar)
     ├── 6. Upload         (artifact → AWS S3)
     └── 7. Deploy         (AWS EC2 — dev/staging/prod)
```

## Key Features

- **100% build pass rate** across multiple Java versions using modular `pom.xml` profiles
- **90%+ JUnit test coverage** — reliable regression detection on every commit
- **SonarQube integration** — enforces code quality gates before deployment
- **Multi-environment deployments** — separate AWS EC2 instances for dev, staging, and production
- **80% reduction in environment-specific bugs** through consistent deployment configuration
- **Automated artifact management** — build artifacts stored and versioned in AWS S3

## Repository Structure

```
CI-CD-Pipeline/
│
├── java-project/           # Java application source code
│   ├── src/
│   │   ├── main/java/      # Application code
│   │   └── test/java/      # JUnit test classes
│   └── pom.xml             # Maven build config with multi-version profiles
│
├── Jenkinsfile             # Jenkins pipeline definition
├── .github/
│   └── workflows/          # GitHub Actions workflow files
└── README.md
```

## Setup & Configuration

### Prerequisites
- Jenkins installed and running
- AWS account with EC2 and S3 access
- Java 11+ installed
- Maven 3.6+
- SonarQube server running

### Jenkins Pipeline Setup

1. Install required Jenkins plugins: Maven Integration, AWS Steps, SonarQube Scanner
2. Configure AWS credentials in Jenkins credentials store
3. Add SonarQube server URL in Jenkins system configuration
4. Create a new Pipeline job → point to this repository's `Jenkinsfile`

### Maven Profiles

```xml
<!-- pom.xml — multi-Java version profiles -->
<profiles>
  <profile>
    <id>java11</id>
    <properties>
      <maven.compiler.source>11</maven.compiler.source>
      <maven.compiler.target>11</maven.compiler.target>
    </properties>
  </profile>
  <profile>
    <id>java17</id>
    <properties>
      <maven.compiler.source>17</maven.compiler.source>
      <maven.compiler.target>17</maven.compiler.target>
    </properties>
  </profile>
</profiles>
```

## Results

| Metric | Result |
|--------|--------|
| Build Pass Rate | 100% across Java 11, 17 |
| Test Coverage | 90%+ (JUnit) |
| Environment Bugs Reduced | 80% |
| Deployment Time | Automated — minutes vs manual hours |

## Key Concepts

- **CI (Continuous Integration):** Automatically build and test code on every commit — catch bugs early
- **CD (Continuous Deployment):** Automatically deploy tested code to environments — no manual steps
- **SonarQube Quality Gate:** Code must meet quality standards before deployment proceeds
- **Maven Profiles:** Same codebase builds correctly across different Java versions
- **AWS S3 as Artifact Store:** Build artifacts versioned and stored — easy rollback if needed

## Author

**Kousalya Kadimella**
MS Computer Science, California State University Dominguez Hills | [GitHub](https://github.com/KousalyaK03)
