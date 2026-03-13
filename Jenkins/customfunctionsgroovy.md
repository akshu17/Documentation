# Writing Custom Functions in Groovy for Jenkins Pipelines

## 1. Overview

In **Jenkins Pipelines**, you can write **custom functions using Groovy** to reuse logic, reduce repetition, and make pipelines cleaner and easier to maintain.

Custom functions can be written in:

* The **same Jenkinsfile**
* **Shared Libraries** (for reusable functions across pipelines)

---

# 2. Why Use Custom Functions?

Benefits:

* Avoid repeating the same code in multiple stages
* Improve pipeline readability
* Make pipelines easier to maintain
* Enable reusable pipeline logic

Example use cases:

* Reusable **build functions**
* **Deployment functions**
* **Notification functions**
* **Artifact upload functions**

---

# 3. Basic Syntax of a Groovy Function

```groovy
def functionName(parameters) {
    // function logic
}
```

Example:

```groovy
def sayHello(name) {
    echo "Hello ${name}"
}
```

---

# 4. Example Jenkinsfile with Custom Function

```groovy
def buildApp() {
    sh 'mvn clean package'
}

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    buildApp()
                }
            }
        }
    }
}
```

Explanation:

* `buildApp()` is a **custom function**
* The function is called inside a **script block**

---

# 5. Function with Parameters

Custom functions can accept parameters.

Example:

```groovy
def deployApp(environment) {
    echo "Deploying application to ${environment}"
}
```

Usage:

```groovy
pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
                script {
                    deployApp("dev")
                }
            }
        }
    }
}
```

Output:

```
Deploying application to dev
```

---

# 6. Function Returning Values

Functions can also return values.

Example:

```groovy
def getVersion() {
    return "1.0.0"
}
```

Usage:

```groovy
script {
    def version = getVersion()
    echo "Application version: ${version}"
}
```

---

# 7. Example: Reusable Build and Upload Functions

```groovy
def buildJar() {
    sh 'mvn clean package'
}

def uploadToS3(bucket) {
    sh "aws s3 cp target/*.jar s3://${bucket}/"
}

pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage('Upload') {
            steps {
                script {
                    uploadToS3("my-jar-bucket")
                }
            }
        }

    }
}
```

---

# 8. Using Functions with Shared Libraries

For large organizations, functions are stored in **Jenkins Shared Libraries**.

Example structure:

```
(shared-library)
│
├── vars
│   └── deployApp.groovy
│
└── src
```

Example function:

```groovy
def call(String env) {
    echo "Deploying to ${env}"
}
```

Usage in Jenkinsfile:

```groovy
@Library('my-shared-lib') _
deployApp('prod')
```

Benefits:

* Centralized reusable functions
* Used across multiple pipelines
* Easier maintenance

---

# 9. Important Notes

* Custom functions must be called inside a **script block** in declarative pipelines.
* Functions should be defined **above the pipeline block**.
* Use **Shared Libraries** for large reusable code.

---

# 10. Best Practices

✔ Keep functions small and focused
✔ Use parameters instead of hardcoding values
✔ Store reusable logic in shared libraries
✔ Avoid complex logic inside Jenkinsfiles

---

# 11. Summary

Yes, in Jenkins you can write **custom functions using Groovy** to improve pipeline reusability and maintainability.

Custom functions allow you to:

* Encapsulate repeated pipeline logic
* Pass parameters
* Return values
* Reuse code across stages or pipelines
