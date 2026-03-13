# Jenkins Pipeline - Stage Failure Handling

---

## Table of Contents
1. [Overview](#1-overview)
2. [Method 1: catchError](#2-method-1-catcherror-simple)
3. [Method 2: try-catch](#3-method-2-try-catch-advanced)
4. [Method 3: failFast](#4-method-3-failfast)
5. [Build Results Explained](#5-build-results-explained)
6. [catchError Options](#6-catcherror-options)
7. [Real World Examples](#7-real-world-examples)
8. [Best Practices](#8-best-practices)
9. [Quick Reference](#9-quick-reference)

---

## 1. Overview

### Default Behavior (Without Error Handling):
```
Stage 1: Build  → SUCCESS ✅
Stage 2: Test   → FAILS ❌
Stage 3: Deploy → NEVER RUNS 🛑
```

### With Error Handling:
```
Stage 1: Build  → SUCCESS ✅
Stage 2: Test   → FAILS ❌ (but continues)
Stage 3: Deploy → STILL RUNS ✅
```

### Simple Rule:
```
Normal Pipeline:
    Stage fails → Pipeline STOPS ❌

With catchError/try-catch:
    Stage fails → Pipeline CONTINUES ✅
```

---

## 2. Method 1: catchError (Simple)

### What is catchError?
```
Catches the error in a stage
Marks stage as failed
But allows pipeline to continue ✅
```

### Basic Syntax:
```groovy
catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
    // your steps here
}
```

### Complete Example:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Build Started'
                echo 'Build Completed ✅'
            }
        }
        stage('Test') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    echo 'Test Started'
                    sh 'exit 1'   // This will FAIL ❌
                    echo 'This line will not run'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy Started'
                echo 'Deploy Completed ✅'
            }
        }
    }
    post {
        success {
            echo 'All Passed ✅'
        }
        unstable {
            echo 'Some stages failed ⚠️'
        }
        failure {
            echo 'Pipeline Failed ❌'
        }
    }
}
```

### What Happens:
```
Build  → SUCCESS ✅
Test   → FAILS ❌ (caught by catchError)
Deploy → STILL RUNS ✅
Result → UNSTABLE ⚠️
```

---

## 3. Method 2: try-catch (Advanced)

### What is try-catch?
```
Groovy's error handling
More control over what
happens when error occurs ✅
```

### Basic Syntax:
```groovy
script {
    try {
        // code that might fail
    } catch (Exception e) {
        echo "Error: ${e.message}"
        // handle the error
    } finally {
        // always runs
    }
}
```

### Complete Example:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Build Completed ✅'
            }
        }
        stage('Test') {
            steps {
                script {
                    try {
                        echo 'Test Started'
                        sh 'exit 1'   // This FAILS ❌
                        echo 'Test Completed'
                    } catch (Exception e) {
                        echo "Test Failed: ${e.message} ❌"
                        echo "Continuing to next stage..."
                        currentBuild.result = 'UNSTABLE'
                    } finally {
                        echo 'Test stage finished (always runs)'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy Started'
                echo 'Deploy Completed ✅'
            }
        }
    }
}
```

### What Happens:
```
Build  → SUCCESS ✅
Test   → FAILS ❌
         → catch block runs
         → "Test Failed" printed
         → build marked UNSTABLE
Deploy → STILL RUNS ✅
```

### try-catch-finally Explained:
```groovy
try {
    // Code that might fail
    // If fails → goes to catch
}
catch (Exception e) {
    // Runs ONLY if error occurs
    // Handle the error here
}
finally {
    // ALWAYS runs
    // Whether error or not
    // Good for cleanup
}
```

---

## 4. Method 3: failFast

### What is failFast?
```
Used in Parallel stages
If one parallel stage fails
Other parallel stages STOP ✅
```

### failFast: true (Stop all on failure)
```groovy
pipeline {
    agent any
    stages {
        stage('Parallel Tests') {
            failFast true   // Stop all if one fails
            parallel {
                stage('Unit Test') {
                    steps {
                        echo 'Running Unit Tests...'
                        sh 'exit 1'   // This FAILS
                    }
                }
                stage('Integration Test') {
                    steps {
                        echo 'Running Integration Tests...'
                        sleep 10   // This gets STOPPED
                    }
                }
            }
        }
    }
}
```

### failFast: false (Continue all on failure)
```groovy
pipeline {
    agent any
    stages {
        stage('Parallel Tests') {
            failFast false   // Continue all even if one fails
            parallel {
                stage('Unit Test') {
                    steps {
                        echo 'Running Unit Tests...'
                        sh 'exit 1'   // This FAILS ❌
                    }
                }
                stage('Integration Test') {
                    steps {
                        echo 'Running Integration Tests...'
                        echo 'Integration Tests Done ✅'
                        // This CONTINUES even if Unit Test fails
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy Completed ✅'
            }
        }
    }
}
```

---

## 5. Build Results Explained

| Result | Symbol | Meaning |
|--------|--------|---------|
| `SUCCESS` | ✅ | Everything passed |
| `UNSTABLE` | ⚠️ | Some issues but continued |
| `FAILURE` | ❌ | Pipeline failed completely |
| `ABORTED` | 🛑 | Manually stopped |
| `NOT_BUILT` | ⏭️ | Stage was skipped |

### How to Set Build Result:
```groovy
// Set to unstable
currentBuild.result = 'UNSTABLE'

// Set to failure
currentBuild.result = 'FAILURE'

// Set to success
currentBuild.result = 'SUCCESS'
```

---

## 6. catchError Options

### buildResult Options:
```groovy
// Overall pipeline result
buildResult: 'SUCCESS'    // Pipeline shows SUCCESS
buildResult: 'UNSTABLE'   // Pipeline shows UNSTABLE ⚠️
buildResult: 'FAILURE'    // Pipeline shows FAILURE ❌
```

### stageResult Options:
```groovy
// Individual stage result
stageResult: 'SUCCESS'    // Stage shows SUCCESS
stageResult: 'UNSTABLE'   // Stage shows UNSTABLE ⚠️
stageResult: 'FAILURE'    // Stage shows FAILURE ❌
```

### Common Combinations:

| buildResult | stageResult | Meaning |
|-------------|-------------|---------|
| UNSTABLE | FAILURE | Stage fails, pipeline continues as unstable |
| SUCCESS | FAILURE | Stage fails, pipeline continues as success |
| FAILURE | FAILURE | Stage fails, pipeline fails but continues |

### Example with Options:
```groovy
stage('Test') {
    steps {
        catchError(
            buildResult: 'UNSTABLE',   // Overall pipeline = UNSTABLE
            stageResult: 'FAILURE',    // This stage = FAILURE
            catchInterruptions: false  // Don't catch interruptions
        ) {
            sh 'run-tests.sh'
        }
    }
}
```

---

## 7. Real World Examples

### Example 1: Continue Deployment Even if Tests Fail
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Application...'
            }
        }
        stage('Unit Tests') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    sh './run-unit-tests.sh'
                }
            }
        }
        stage('Integration Tests') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    sh './run-integration-tests.sh'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging regardless...'
                sh './deploy-staging.sh'
            }
        }
    }
    post {
        unstable {
            echo '⚠️ Some tests failed but deployed to staging'
        }
        success {
            echo '✅ All tests passed and deployed'
        }
    }
}
```

### Example 2: Multiple Stages with Error Handling
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
            }
        }
        stage('Build') {
            steps {
                script {
                    try {
                        echo 'Building...'
                        sh './build.sh'
                    } catch (Exception e) {
                        echo "Build failed: ${e.message}"
                        currentBuild.result = 'UNSTABLE'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    try {
                        echo 'Testing...'
                        sh './test.sh'
                    } catch (Exception e) {
                        echo "Tests failed: ${e.message}"
                        currentBuild.result = 'UNSTABLE'
                    }
                }
            }
        }
        stage('Code Quality') {
            steps {
                script {
                    try {
                        echo 'Running Code Quality checks...'
                        sh './sonar-scan.sh'
                    } catch (Exception e) {
                        echo "Quality check failed: ${e.message}"
                        currentBuild.result = 'UNSTABLE'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh './deploy.sh'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo '✅ All stages passed!'
        }
        unstable {
            echo '⚠️ Pipeline completed with some failures'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
```

### Example 3: Parallel Tests with Error Handling
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Build Completed ✅'
            }
        }
        stage('All Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        catchError(
                            buildResult: 'UNSTABLE',
                            stageResult: 'FAILURE'
                        ) {
                            echo 'Running Unit Tests...'
                            sh './unit-tests.sh'
                        }
                    }
                }
                stage('Integration Tests') {
                    steps {
                        catchError(
                            buildResult: 'UNSTABLE',
                            stageResult: 'FAILURE'
                        ) {
                            echo 'Running Integration Tests...'
                            sh './integration-tests.sh'
                        }
                    }
                }
                stage('Performance Tests') {
                    steps {
                        catchError(
                            buildResult: 'UNSTABLE',
                            stageResult: 'FAILURE'
                        ) {
                            echo 'Running Performance Tests...'
                            sh './performance-tests.sh'
                        }
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying Application ✅'
            }
        }
    }
}
```

---

## 8. Best Practices

### DO's ✅
```
✅ Use catchError for non-critical stages
✅ Use try-catch for complex error handling
✅ Always set meaningful build results
✅ Add post section for notifications
✅ Log error messages clearly
✅ Use UNSTABLE for warnings
✅ Use FAILURE for critical errors
```

### DON'Ts ❌
```
❌ Don't ignore all errors blindly
❌ Don't continue if critical stages fail
❌ Don't forget to notify team of failures
❌ Don't use catchError for security checks
❌ Don't skip errors in production deploys
```

### When to Continue on Failure:
```
✅ Test stages (non-blocking)
✅ Code quality checks
✅ Optional notifications
✅ Cleanup stages
✅ Reporting stages
```

### When to STOP on Failure:
```
❌ Build stage fails
❌ Security scan fails
❌ Critical tests fail
❌ Production deployment fails
❌ Authentication fails
```

---

## 9. Quick Reference

### catchError:
```groovy
catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
    // steps that might fail
}
```

### try-catch:
```groovy
script {
    try {
        // steps that might fail
    } catch (Exception e) {
        echo "Error: ${e.message}"
        currentBuild.result = 'UNSTABLE'
    }
}
```

### failFast in Parallel:
```groovy
stage('Parallel') {
    failFast false   // Continue all parallel stages
    parallel {
        stage('A') { steps { ... } }
        stage('B') { steps { ... } }
    }
}
```

### Set Build Result:
```groovy
currentBuild.result = 'UNSTABLE'  // ⚠️
currentBuild.result = 'FAILURE'   // ❌
currentBuild.result = 'SUCCESS'   // ✅
```

### Post Section:
```groovy
post {
    always   { echo 'Always runs' }
    success  { echo 'Only on success ✅' }
    failure  { echo 'Only on failure ❌' }
    unstable { echo 'Only on unstable ⚠️' }
    aborted  { echo 'Only if aborted 🛑' }
}
```

---

## Summary

```
┌─────────────────────────────────────────┐
│         ERROR HANDLING METHODS          │
│                                         │
│  Method 1: catchError                   │
│  → Simple and easy ✅                   │
│  → Best for most cases                  │
│                                         │
│  Method 2: try-catch                    │
│  → More control ✅                      │
│  → Best for complex handling            │
│                                         │
│  Method 3: failFast                     │
│  → For parallel stages ✅               │
│  → Control parallel behavior            │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│         STAGE FAILURE FLOW              │
│                                         │
│  Without Error Handling:                │
│  Build ✅ → Test ❌ → Deploy 🛑         │
│                                         │
│  With Error Handling:                   │
│  Build ✅ → Test ❌ → Deploy ✅         │
└─────────────────────────────────────────┘
```

---

*Notes compiled - March 2026*
