# Maven Build Commands and Email Notification in Jenkins

## 1. Maven Build Commands for Java

**Maven** is a build automation tool used primarily for Java projects. It manages project builds, dependencies, and packaging.

### Common Maven Commands

| Command       | Description                                 |
| ------------- | ------------------------------------------- |
| `mvn clean`   | Removes previous build files                |
| `mvn compile` | Compiles the source code                    |
| `mvn test`    | Executes unit tests                         |
| `mvn package` | Packages code into JAR/WAR                  |
| `mvn install` | Installs artifact into the local repository |

### Most Common Build Command

```bash
mvn clean install
```

### Build Flow

```text
Source Code → Compile → Test → Package → Install
```

Example generated artifact:

```text
target/application.jar
```

---

# 2. Build Commands for Python Projects

Python projects usually use **pip**, **setuptools**, or testing frameworks.

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run Tests

```bash
pytest
```

### Build Python Package

```bash
python setup.py build
```

### Example Python CI Steps

```bash
pip install -r requirements.txt
pytest
```

---

# 3. Sending Email Notifications in Jenkins

Jenkins can send automatic email notifications when a build:

* Succeeds
* Fails
* Becomes unstable
* Is aborted

This is typically done using the **Email Extension Plugin**.

---

# 4. Install Email Extension Plugin

Steps:

1. Go to **Manage Jenkins**
2. Click **Manage Plugins**
3. Select **Available Plugins**
4. Search for **Email Extension Plugin**
5. Install the plugin

---

# 5. Configure SMTP Email Settings

Navigate to:

```text
Manage Jenkins → Configure System
```

Configure SMTP server details.

Example configuration:

| Field       | Example                                             |
| ----------- | --------------------------------------------------- |
| SMTP Server | smtp.gmail.com                                      |
| SMTP Port   | 587                                                 |
| Username    | [your-email@gmail.com](mailto:your-email@gmail.com) |
| Password    | app password                                        |

---

# 6. Jenkins Pipeline Example for Email Notification

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building application..."
            }
        }
    }

    post {

        success {
            emailext(
                subject: "Build Successful",
                body: "The Jenkins build completed successfully.",
                to: "team@example.com"
            )
        }

        failure {
            emailext(
                subject: "Build Failed",
                body: "The Jenkins build has failed. Please check the logs.",
                to: "team@example.com"
            )
        }

    }
}
```

---

# 7. Email Notification Workflow

```text
Developer pushes code
        ↓
Jenkins pipeline starts
        ↓
Build and tests execute
        ↓
Build status generated
        ↓
Email notification sent to team
```

---

# 8. Types of Email Notifications

| Event          | Notification       |
| -------------- | ------------------ |
| Build Success  | Success email sent |
| Build Failure  | Failure alert sent |
| Unstable Build | Warning email sent |
| Build Aborted  | Notification email |

---

# 9. Best Practices

* Send notifications mainly for **failures or unstable builds**
* Use **team email groups** instead of individual emails
* Include **build links and logs** in emails
* Combine with chat notifications (Slack / Teams) for faster alerts

---

# 10. Summary

* Maven is used to build Java applications using commands like `mvn clean install`.
* Python projects typically use `pip install`, `pytest`, and `setup.py build`.
* Jenkins can send build status notifications using the **Email Extension Plugin**.
* Email notifications help teams quickly identify build failures and pipeline issues.
