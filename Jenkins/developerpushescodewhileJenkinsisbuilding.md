# Jenkins Scenario: Code Pushed While Build is Running on Dev Branch

## 1. Scenario Description

A common situation in CI/CD pipelines:

* Jenkins is **building code from the `dev` branch**
* The **build is currently in progress**
* Meanwhile, **another developer pushes new code to the same `dev` branch**

This raises the question:

> What happens to the Jenkins build that is already running?

---

# 2. Default Jenkins Behavior

By default, Jenkins behaves as follows:

1. Jenkins **checks out the code at the time the build started**
2. The current build **continues using that snapshot of the repository**
3. The new commit **does not affect the running build**

### Important Point

The running build is **isolated from new commits**.

Example timeline:

```id="1stf9n"
Time 10:00 → Jenkins build starts (Commit A)
Time 10:02 → Developer pushes Commit B
Time 10:05 → Jenkins finishes building Commit A
```

Result:

* Jenkins build uses **Commit A**
* Commit B will be built in **next build trigger**

---

# 3. How Jenkins Detects the New Commit

If the pipeline is configured with:

* **Git Webhooks**
* **Polling SCM**
* **Multibranch Pipeline**

Then Jenkins will detect the new commit and:

* Trigger **another build**
* Add it to the **build queue**

Example:

```id="moa2k9"
Build #101 → Building Commit A (running)

Commit B pushed

Build #102 → Triggered and queued
```

---

# 4. Possible Build Handling Strategies

## Strategy 1: Allow Multiple Builds

Jenkins runs multiple builds sequentially or in parallel depending on configuration.

Example:

```id="7qsdic"
Build #101 → Commit A
Build #102 → Commit B
```

---

## Strategy 2: Cancel Previous Build

Sometimes teams prefer **building only the latest commit**.

This can be achieved using:

* `disableConcurrentBuilds()`
* **Throttle builds**
* **Abort previous builds plugin**

Example:

```groovy id="fcnhx8"
options {
    disableConcurrentBuilds()
}
```

Result:

* If a new commit arrives
* The previous build can be **aborted or queued**

---

## Strategy 3: Build Only Latest Commit

Plugins like:

* **Build Blocker**
* **Quiet Period**
* **Milestone Step**

Example using milestone:

```groovy id="v9sn22"
milestone 1
```

This ensures **older builds are automatically aborted** when newer builds reach the milestone.

---

# 5. Best Practice in CI/CD

Recommended approach:

✔ Allow builds to finish using the commit snapshot
✔ Trigger new builds for new commits
✔ Avoid modifying running builds

Large teams often implement:

* **Queue builds**
* **Abort outdated builds**
* **Build only the latest commit**

---

# 6. Example Pipeline Protection

Example Jenkinsfile snippet:

```groovy id="pd1sy1"
pipeline {
    agent any

    options {
        disableConcurrentBuilds()
    }

    stages {
        stage('Build') {
            steps {
                echo "Building current commit"
            }
        }
    }
}
```

---

# 7. Summary

If a developer pushes code while Jenkins is building:

* The **current build continues with the old commit**
* The **new commit triggers a new build**
* Jenkins **does not interrupt the running build by default**

This ensures **build consistency and reproducibility** in CI/CD pipelines.
