# Jenkins Build – Overview

## 1. What is a Jenkins Build?

A **Jenkins build** is the process where Jenkins executes a series of automated steps to **compile, test, package, or deploy an application**.

It is a key part of **Continuous Integration (CI)** and **Continuous Delivery (CD)** pipelines.

Example tasks in a Jenkins build:

* Pull code from a repository
* Compile source code
* Run automated tests
* Package artifacts (JAR/WAR/Docker image)
* Deploy to environments

---

# 2. Jenkins Build Workflow

Typical Jenkins build workflow:

```text
Developer pushes code → Git Repository
             ↓
        Jenkins Trigger
             ↓
      Checkout Source Code
             ↓
           Build
             ↓
            Test
             ↓
        Package Artifact
             ↓
           Deploy
```

---

# 3. Types of Jenkins Builds

## 1. Manual Build

A build triggered manually by a user.

Steps:

1. Open Jenkins Dashboard
2. Select the Job
3. Click **Build Now**

---

## 2. Scheduled Build

Builds run at scheduled times using **cron expressions**.

Example:

```groovy
triggers {
    cron('H/15 * * * *')
}
```

This triggers a build **every 15 minutes**.

---

## 3. SCM Triggered Build

Triggered when code changes are detected in a **source control system** like Git.

Methods:

* Git Webhooks
* Poll SCM

Example:

```groovy
triggers {
    pollSCM('H/5 * * * *')
}
```

This checks the repository every **5 minutes**.

---

## 4. Upstream Build

Triggered after another job finishes.

Example:

* Build Job A
* After success → Trigger Job B

---

# 4. Jenkins Build Stages (Pipeline)

Example pipeline:

```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/example/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
            }
        }

    }
}
```

Stages include:

* Checkout
* Build
* Test
* Deploy

---

# 5. Jenkins Build Status

Each build has a status:

| Status   | Meaning                          |
| -------- | -------------------------------- |
| SUCCESS  | Build completed successfully     |
| FAILURE  | Build failed                     |
| UNSTABLE | Tests failed but build completed |
| ABORTED  | Build was manually stopped       |

---

# 6. Jenkins Build Artifacts

Artifacts are files generated during a build.

Examples:

* `.jar`
* `.war`
* `.zip`
* Docker images

Example artifact archiving:

```groovy
post {
    success {
        archiveArtifacts artifacts: 'target/*.jar'
    }
}
```

---

# 7. Jenkins Build History

Jenkins keeps a history of builds:

```text
Build #101
Build #102
Build #103
```

Each build stores:

* Console logs
* Artifacts
* Build status
* Execution time

---

# 8. Benefits of Jenkins Builds

* Automated software building
* Faster feedback for developers
* Improved code quality
* Continuous integration
* Easy deployment automation

---

# 9. Summary

A **Jenkins build** is an automated process that:

1. Fetches code from a repository
2. Compiles and tests the application
3. Packages artifacts
4. Deploys the application

It helps teams implement **CI/CD practices for faster and reliable software delivery**.
