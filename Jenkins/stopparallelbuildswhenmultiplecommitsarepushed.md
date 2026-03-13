# Preventing Parallel Builds in Jenkins When Multiple Commits Are Pushed

## 1. Problem Scenario

In a CI/CD pipeline:

* Jenkins is building code from a branch (e.g., `dev`)
* Another developer pushes new code to the same branch
* Jenkins triggers **another build**

This may lead to **multiple builds running in parallel**, which can cause:

* Resource wastage
* Deployment conflicts
* Unstable environments

---

# 2. Solution: Disable Parallel Builds

To stop parallel builds in Jenkins, you can use the **`disableConcurrentBuilds()`** option in the Jenkins pipeline.

This ensures that **only one build runs at a time** for a job.

---

# 3. Jenkinsfile Example

```groovy id="1p9hbe"
pipeline {
    agent any

    options {
        disableConcurrentBuilds()
    }

    stages {
        stage('Build') {
            steps {
                echo "Building application..."
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }
    }
}
```

---

# 4. How It Works

When a new commit triggers a build:

| Situation               | Behavior                       |
| ----------------------- | ------------------------------ |
| Build already running   | New build waits in queue       |
| Current build finishes  | Next build starts              |
| Multiple commits pushed | Builds are queued sequentially |

Example timeline:

```id="q2e6nj"
Commit A → Build #101 (Running)

Commit B → Build #102 (Queued)

Commit C → Build #103 (Queued)
```

---

# 5. Alternative Solution: Abort Previous Builds

Sometimes teams prefer building **only the latest commit**.

This can be done using **milestones**.

Example:

```groovy id="e8b3qj"
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                milestone 1
                echo "Building latest commit"
            }
        }
    }
}
```

Result:

* Older builds will be **aborted**
* Only the **latest build continues**

---

# 6. Another Method: Jenkins Job Configuration

In **Freestyle Jobs**:

Navigate to:

```id="91t0hu"
Job Configuration → Build Environment
```

Enable:

```
Do not allow concurrent builds
```

This ensures Jenkins runs **only one build at a time**.

---

# 7. Best Practice in CI/CD

Recommended strategies:

✔ Use **disableConcurrentBuilds()** to avoid parallel builds
✔ Use **milestones** to stop outdated builds
✔ Build **only the latest commit** in fast-moving repositories

---

# 8. Summary

To stop parallel builds when multiple commits are pushed:

* Use **`disableConcurrentBuilds()`** in Jenkins pipeline
* Jenkins will **queue builds instead of running them simultaneously**
* Optionally use **milestones to abort outdated builds**

This helps maintain **pipeline stability and efficient resource usage**.
