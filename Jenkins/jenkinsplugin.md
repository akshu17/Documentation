# Common Jenkins Plugins Used in CI/CD

## 1. Overview

Jenkins plugins extend the functionality of Jenkins and enable integration with various tools used in **DevOps pipelines**, such as Git, Docker, SonarQube, AWS, and Kubernetes.

Below are some commonly used Jenkins plugins in real-world CI/CD environments.

---

# 2. Git Plugin

**Purpose:**
Integrates Jenkins with Git repositories.

Features:

* Clone repositories
* Pull latest code
* Trigger builds on commits

Example usage:

```groovy
git 'https://github.com/example/repo.git'
```

---

# 3. Pipeline Plugin

**Purpose:**
Allows writing Jenkins pipelines using **Jenkinsfile (Groovy syntax)**.

Features:

* Declarative pipelines
* Scripted pipelines
* Stage-based builds

Example:

```groovy
pipeline {
  agent any
  stages {
    stage('Build'){
      steps{
        echo "Building application"
      }
    }
  }
}
```

---

# 4. SonarQube Scanner Plugin

**Purpose:**
Integrates Jenkins with SonarQube for **static code analysis**.

Features:

* Code quality scanning
* Security vulnerability detection
* Quality gate validation

Example:

```groovy
withSonarQubeEnv('SonarQube') {
    sh 'mvn sonar:sonar'
}
```

---

# 5. Docker Plugin

**Purpose:**
Allows Jenkins to build and manage Docker containers.

Features:

* Build Docker images
* Run containers
* Push images to Docker registries

Example:

```groovy
sh 'docker build -t myapp .'
```

---

# 6. AWS Credentials Plugin

**Purpose:**
Manages AWS credentials securely inside Jenkins.

Used for:

* S3 uploads
* EC2 deployments
* ECR authentication

Example:

```groovy
withCredentials([[
$class: 'AmazonWebServicesCredentialsBinding',
credentialsId: 'aws-credentials'
]])
```

---

# 7. Kubernetes Plugin

**Purpose:**
Allows Jenkins to run builds inside **Kubernetes pods**.

Features:

* Dynamic agents
* Containerized build environments
* Scalable pipelines

---

# 8. Blue Ocean Plugin

**Purpose:**
Provides a **modern UI for Jenkins pipelines**.

Features:

* Visual pipeline editor
* Better pipeline visualization
* Easier debugging

---

# 9. Email Extension Plugin

**Purpose:**
Send email notifications based on build results.

Example:

```groovy
emailext (
 subject: "Build Status",
 body: "Build completed",
 to: "team@example.com"
)
```

---

# 10. Slack Notification Plugin

**Purpose:**
Send build notifications to **Slack channels**.

Example:

```groovy
slackSend channel: '#devops', message: 'Build Successful'
```

---

# 11. Artifactory Plugin

**Purpose:**
Integrates Jenkins with artifact repositories.

Used for storing:

* JAR files
* WAR files
* Docker images
* Build artifacts

---

# 12. Credentials Binding Plugin

**Purpose:**
Securely store and access credentials like:

* API keys
* Passwords
* Tokens

Example:

```groovy
withCredentials([string(credentialsId: 'token', variable: 'API_TOKEN')]) {
    sh 'echo $API_TOKEN'
}
```

---

# 13. Build Timeout Plugin

**Purpose:**
Automatically stops builds that run too long.

Example configuration:

```groovy
options {
    timeout(time: 30, unit: 'MINUTES')
}
```

---

# 14. Copy Artifact Plugin

**Purpose:**
Copies artifacts from one Jenkins job to another.

Useful in **multi-job pipelines**.

---

# 15. Summary

Common Jenkins plugins used in DevOps pipelines include:

| Plugin                 | Purpose                  |
| ---------------------- | ------------------------ |
| Git Plugin             | Source code integration  |
| Pipeline Plugin        | CI/CD pipeline creation  |
| SonarQube Scanner      | Code quality analysis    |
| Docker Plugin          | Container builds         |
| AWS Credentials Plugin | AWS authentication       |
| Kubernetes Plugin      | Dynamic build agents     |
| Blue Ocean             | Pipeline visualization   |
| Email Extension        | Email notifications      |
| Slack Plugin           | Slack alerts             |
| Credentials Binding    | Secure secret management |

These plugins help Jenkins integrate with **modern DevOps tools and automate the entire software delivery pipeline**.
