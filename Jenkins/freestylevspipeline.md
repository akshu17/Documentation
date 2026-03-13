# Freestyle vs Pipeline Job in Jenkins

--
## Table of Contents
1. [What is Freestyle Job?](#1-what-is-freestyle-job)
2. [What is Pipeline Job?](#2-what-is-pipeline-job)
3. [Key Differences](#3-key-differences)
4. [Freestyle Job - Deep Dive](#4-freestyle-job---deep-dive)
5. [Pipeline Job - Deep Dive](#5-pipeline-job---deep-dive)
6. [When to Use Which?](#6-when-to-use-which)
7. [Real World Examples](#7-real-world-examples)
8. [Pipeline Types](#8-pipeline-types)
9. [Complete Pipeline Examples](#9-complete-pipeline-examples)
10. [Quick Reference](#10-quick-reference)

---

## 1. What is Freestyle Job?

```
A simple Jenkins job where you
configure everything by clicking
buttons and filling forms.
No coding required! ✅
```

### Simple Explanation:
```
Think of Freestyle like:
→ Filling a form ✅
→ Clicking checkboxes ✅
→ No programming needed ✅
```

### How it looks:
```
Jenkins Dashboard
    → New Item
        → Freestyle Project
            → Fill form fields
            → Click buttons
            → Done! ✅
```

---

## 2. What is Pipeline Job?

```
A Jenkins job where you write
a script (Groovy code) to define
your entire CI/CD process. ✅
```

### Simple Explanation:
```
Think of Pipeline like:
→ Writing a recipe 📝
→ Step by step instructions
→ More control and flexibility ✅
```

### How it looks:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
```

---

## 3. Key Differences

| Feature | Freestyle | Pipeline |
|---------|-----------|----------|
| **Setup** | Click buttons | Write code |
| **Coding** | Not required | Required (Groovy) |
| **Stages** | Not available | Available ✅ |
| **Parallel execution** | Not available | Available ✅ |
| **Conditions (if/else)** | Very limited | Full support ✅ |
| **Version control** | Cannot store in Git | Can store in Git ✅ |
| **Visualization** | Limited | Full stage view ✅ |
| **Reusability** | Cannot reuse | Can reuse code ✅ |
| **Complexity** | Simple | Can be complex |
| **Learning curve** | Easy | Medium |
| **Error handling** | Limited | Full support ✅ |
| **Parameters** | Basic | Advanced ✅ |
| **Best for** | Beginners | Production |
| **Maintenance** | Hard to maintain | Easy to maintain ✅ |
| **Audit trail** | Limited | Full history ✅ |

---

## 4. Freestyle Job - Deep Dive

### What you can configure:
```
1. General Settings
   → Job description
   → Parameters (basic)
   → Throttle builds

2. Source Code Management
   → Git repository URL
   → Credentials
   → Branch

3. Build Triggers
   → Poll SCM
   → Schedule
   → GitHub webhook
   → Upstream/Downstream

4. Build Environment
   → Delete workspace
   → Set environment variables
   → Timestamps

5. Build Steps
   → Execute Shell
   → Execute Windows batch
   → Invoke Maven
   → Copy artifacts

6. Post Build Actions
   → Archive artifacts
   → Send email
   → Trigger other jobs
   → Publish reports
```

### Example Freestyle Job:
```
Name: SimpleWebDeploy
Source Code: Git → https://github.com/user/repo.git
Build Trigger: GitHub Webhook
Build Step: Execute Shell
    → ./build.sh
Post Build: Send Email notification
```

### Advantages:
```
✅ Easy to setup
✅ No coding knowledge needed
✅ Quick to configure
✅ Good for learning
✅ Simple tasks
```

### Disadvantages:
```
❌ Cannot store in Git
❌ Hard to maintain
❌ Limited flexibility
❌ No parallel execution
❌ No complex conditions
❌ Difficult to replicate
```

---

## 5. Pipeline Job - Deep Dive

### Two types of Pipeline:

#### Type 1: Declarative Pipeline
```groovy
// Simple, structured, recommended
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
```

#### Type 2: Scripted Pipeline
```groovy
// Advanced, more flexible
node {
    stage('Build') {
        echo 'Building...'
    }
}
```

### Pipeline Features:

#### 1. Stages
```groovy
stages {
    stage('Build')  { ... }
    stage('Test')   { ... }
    stage('Deploy') { ... }
}
```

#### 2. Environment Variables
```groovy
environment {
    APP_NAME = 'MyApp'
    VERSION  = '1.0'
}
```

#### 3. Parameters
```groovy
parameters {
    string(name: 'BRANCH', defaultValue: 'main')
    choice(name: 'ENV', choices: ['Dev', 'Prod'])
    booleanParam(name: 'RUN_TESTS', defaultValue: true)
}
```

#### 4. Parallel Execution
```groovy
stage('Tests') {
    parallel {
        stage('Unit Test')        { ... }
        stage('Integration Test') { ... }
        stage('Performance Test') { ... }
    }
}
```

#### 5. Conditions (When)
```groovy
stage('Deploy') {
    when {
        expression {
            params.ENVIRONMENT == 'Production'
        }
    }
    steps { ... }
}
```

#### 6. Error Handling
```groovy
stage('Build') {
    steps {
        catchError(buildResult: 'SUCCESS') {
            sh 'build.sh'
        }
    }
}
```

#### 7. Post Actions
```groovy
post {
    success { echo 'Success! ✅' }
    failure { echo 'Failed! ❌' }
    always  { echo 'Always runs' }
}
```

### Advantages:
```
✅ Store pipeline as code in Git
✅ Full CI/CD automation
✅ Parallel execution
✅ Advanced conditions
✅ Easy to maintain
✅ Reusable code
✅ Full visualization
✅ Better error handling
✅ Audit trail
```

### Disadvantages:
```
❌ Requires coding knowledge
❌ Steeper learning curve
❌ More complex setup
❌ Need to know Groovy
```

---

## 6. When to Use Which?

### Use Freestyle When:
```
✅ You are a beginner
✅ Simple single task job
✅ Quick setup needed
✅ No coding knowledge
✅ Small/simple projects
✅ One-time tasks
✅ Basic build jobs
```

### Use Pipeline When:
```
✅ Complex CI/CD workflows
✅ Multiple stages needed
✅ Multiple environments
   (Dev, Staging, Production)
✅ Parallel test execution
✅ Advanced conditions needed
✅ Large/enterprise projects
✅ Team collaboration
✅ Need audit trail
✅ Production deployments
✅ Docker/Kubernetes deployments
✅ Microservices architecture
```

### Simple Decision Rule:
```
Simple task?
    → Use Freestyle ✅

Complex CI/CD?
    → Use Pipeline ✅

Not sure?
    → Use Pipeline ✅
       (more flexible for future)
```

---

## 7. Real World Examples

### Example 1: Simple Website (Freestyle)
```
Project: Company website
Task: Pull code and copy to server

Freestyle Setup:
→ Source Code: Git
→ Build Trigger: GitHub Webhook
→ Build Step: Execute Shell
   rsync -av ./ /var/www/html/
→ Post Build: Send email ✅
```

### Example 2: Banking App (Pipeline)
```
Project: Banking Application
Tasks: Build → Test → Deploy

Pipeline Setup:
Stage 1: Checkout code
Stage 2: Build application
Stage 3: Run unit tests
Stage 4: Run integration tests (parallel)
Stage 5: Security scan (parallel)
Stage 6: Build Docker image
Stage 7: Deploy to staging
Stage 8: Run smoke tests
Stage 9: Deploy to production
Stage 10: Send notification ✅
```

### Example 3: Mobile App (Pipeline)
```
Project: Mobile App
Tasks: Different builds for different OS

Pipeline Setup:
Stage 1: Checkout
Stage 2: Parallel Build
    → Build iOS version
    → Build Android version
Stage 3: Parallel Test
    → Test iOS
    → Test Android
Stage 4: Deploy to App Stores ✅
```

---

## 8. Pipeline Types

### Declarative Pipeline (Recommended)
```groovy
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```

### Scripted Pipeline (Advanced)
```groovy
node {
    stage('Example') {
        echo 'Hello World'
    }
}
```

### Comparison:

| Feature | Declarative | Scripted |
|---------|-------------|----------|
| Syntax | Simple | Complex |
| Learning | Easy | Hard |
| Validation | Better | Limited |
| Flexibility | Good | Full |
| Recommended | Yes ✅ | Advanced only |

---

## 9. Complete Pipeline Examples

### Basic Pipeline
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Build Started'
                echo 'Building Application...'
                echo 'Build Completed'
            }
        }
        stage('Test') {
            steps {
                echo 'Test Started'
                echo 'Running Tests...'
                echo 'Test Completed'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy Started'
                echo 'Deploying Application...'
                echo 'Deploy Completed'
            }
        }
    }
    post {
        success {
            echo 'Pipeline Succeeded! ✅'
        }
        failure {
            echo 'Pipeline Failed! ❌'
        }
    }
}
```

### Advanced Pipeline with All Features
```groovy
pipeline {
    agent any

    // Environment Variables
    environment {
        APP_NAME = 'MyApp'
        VERSION  = '1.0'
    }

    // Parameters
    parameters {
        string(
            name: 'BRANCH_NAME',
            defaultValue: 'main',
            description: 'Branch to build'
        )
        choice(
            name: 'ENVIRONMENT',
            choices: ['Development', 'Staging', 'Production'],
            description: 'Target environment'
        )
        booleanParam(
            name: 'RUN_TESTS',
            defaultValue: true,
            description: 'Run tests?'
        )
    }

    stages {

        // Checkout Stage
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "*/${params.BRANCH_NAME}"]],
                    userRemoteConfigs: [[
                        url: 'https://github.com/user/repo.git',
                        credentialsId: 'github-credentials'
                    ]]
                ])
                echo "Checked out: ${params.BRANCH_NAME}"
            }
        }

        // Build Stage
        stage('Build') {
            steps {
                echo "Building ${APP_NAME} v${VERSION}"
            }
        }

        // Parallel Tests
        stage('Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running Unit Tests...'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running Integration Tests...'
                    }
                }
            }
        }

        // Conditional Deploy to Staging
        stage('Deploy Staging') {
            when {
                expression {
                    params.ENVIRONMENT == 'Staging'
                }
            }
            steps {
                echo 'Deploying to Staging...'
            }
        }

        // Conditional Deploy to Production
        stage('Deploy Production') {
            when {
                expression {
                    params.ENVIRONMENT == 'Production'
                }
            }
            steps {
                echo 'Deploying to Production...'
            }
        }
    }

    post {
        success {
            echo "${APP_NAME} Pipeline Succeeded! ✅"
        }
        failure {
            echo "${APP_NAME} Pipeline Failed! ❌"
        }
        always {
            echo 'Pipeline Finished!'
        }
    }
}
```

---

## 10. Quick Reference

### Freestyle Job Setup Steps:
```
1. New Item → Freestyle Project
2. Configure Source Code (Git)
3. Set Build Triggers
4. Add Build Steps (Execute Shell)
5. Add Post Build Actions
6. Save → Build Now ✅
```

### Pipeline Job Setup Steps:
```
1. New Item → Pipeline
2. Scroll to Pipeline section
3. Write/paste Groovy script
4. Save → Build Now ✅
```

### Pipeline Keywords:

| Keyword | Purpose |
|---------|---------|
| `pipeline` | Start of pipeline |
| `agent any` | Run on any agent |
| `stages` | Group of stages |
| `stage('name')` | Single stage |
| `steps` | Commands to run |
| `echo` | Print message |
| `sh` | Run shell command |
| `environment` | Set variables |
| `parameters` | User inputs |
| `when` | Conditions |
| `parallel` | Run in parallel |
| `script` | Groovy code block |
| `post` | After pipeline actions |

### Common Pipeline Commands:
```groovy
// Print message
echo 'Hello World'

// Run shell command
sh 'ls -la'

// Use variable
echo "${APP_NAME}"

// Use parameter
echo "${params.ENVIRONMENT}"

// Conditional
when {
    expression { params.ENV == 'Production' }
}

// Parallel
parallel {
    stage('A') { steps { ... } }
    stage('B') { steps { ... } }
}
```

---

## Summary

```
┌─────────────────────────────────────────────────┐
│              FREESTYLE JOB                       │
│                                                  │
│  ✅ Easy to use                                  │
│  ✅ No coding needed                             │
│  ✅ Good for beginners                           │
│  ❌ Limited features                             │
│  ❌ Cannot store in Git                          │
│  ❌ Hard to maintain                             │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│              PIPELINE JOB                        │
│                                                  │
│  ✅ Full CI/CD automation                        │
│  ✅ Store as code in Git                         │
│  ✅ Parallel execution                           │
│  ✅ Advanced conditions                          │
│  ✅ Easy to maintain                             │
│  ❌ Requires coding knowledge                    │
└─────────────────────────────────────────────────┘
```

---

*Notes compiled - March 2026*
