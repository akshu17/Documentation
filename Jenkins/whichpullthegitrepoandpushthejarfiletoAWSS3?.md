# Jenkins Pipeline: Pull Code from Git and Push JAR to AWS S3

## 1. Objective

Create a **Jenkins Pipeline (Jenkinsfile)** that performs the following tasks:

1. Pulls source code from a **Git repository**
2. Builds the project to generate a **JAR file**
3. Uploads the generated **JAR file to an AWS S3 bucket**

---

# 2. Pipeline Workflow

```
Git Repository
      ↓
Jenkins Checkout Stage
      ↓
Build Stage (Maven)
      ↓
Generate JAR File
      ↓
Upload Artifact to AWS S3
```

---

# 3. Jenkinsfile Example

```groovy
pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/your-username/your-repo.git'
        BRANCH = 'main'
        S3_BUCKET = 'your-s3-bucket-name'
        AWS_REGION = 'us-east-1'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Upload JAR to S3') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {

                    sh '''
                    aws configure set region $AWS_REGION
                    aws s3 cp target/*.jar s3://$S3_BUCKET/
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Build and Upload to S3 Successful!'
        }
        failure {
            echo 'Pipeline Failed!'
        }
    }
}
```

---

# 4. Explanation of Pipeline Stages

## Stage 1: Checkout Code

This stage pulls the source code from the **Git repository**.

```
git branch: "${BRANCH}", url: "${GIT_REPO}"
```

Purpose:

* Connects Jenkins to the Git repository
* Downloads the latest code from the specified branch

---

## Stage 2: Build JAR

```
mvn clean package
```

Purpose:

* Uses **Maven** to build the project
* Generates a **JAR file** inside the `target/` directory

Example output:

```
target/my-application.jar
```

---

## Stage 3: Upload JAR to AWS S3

```
aws s3 cp target/*.jar s3://$S3_BUCKET/
```

Purpose:

* Uses **AWS CLI**
* Uploads the generated JAR file to the specified **S3 bucket**

---

# 5. Jenkins Environment Variables

| Variable     | Description              |
| ------------ | ------------------------ |
| `GIT_REPO`   | Git repository URL       |
| `BRANCH`     | Branch to pull code from |
| `S3_BUCKET`  | Target S3 bucket         |
| `AWS_REGION` | AWS region               |

---

# 6. Prerequisites

## 1. Install Required Tools on Jenkins Agent

The Jenkins server or agent should have:

* **Java**
* **Maven**
* **AWS CLI**

Example installation:

```
sudo apt install maven
sudo apt install awscli
```

---

## 2. Configure AWS Credentials in Jenkins

Navigate to:

```
Manage Jenkins → Credentials → Global → Add Credentials
```

Add:

* **Kind:** AWS Credentials
* **Access Key**
* **Secret Key**
* **Credentials ID:** `aws-credentials`

---

# 7. Create an AWS S3 Bucket

Example command:

```
aws s3 mb s3://your-s3-bucket-name
```

This creates a new **S3 bucket** to store the JAR artifacts.

---

# 8. IAM Permissions Required

The AWS user must have the following permissions:

```json
{
  "Effect": "Allow",
  "Action": [
    "s3:PutObject",
    "s3:GetObject"
  ],
  "Resource": "arn:aws:s3:::your-s3-bucket-name/*"
}
```

Purpose:

* Allows uploading files to S3
* Allows retrieving files from the bucket

---

# 9. Post Pipeline Actions

Jenkins can execute actions after the pipeline completes.

```
post {
    success { ... }
    failure { ... }
}
```

Examples:

* Send notifications
* Trigger another pipeline
* Log pipeline status

---

# 10. Benefits of This Pipeline

* Automated build process
* Continuous integration workflow
* Artifact storage in S3
* Easy integration with deployment pipelines
* Scalable and cloud-friendly

---

# 11. Summary

This Jenkins pipeline automates the following process:

1. Pull code from Git
2. Build the project using Maven
3. Generate a JAR artifact
4. Upload the artifact to AWS S3

Such pipelines are commonly used in **CI/CD systems** to automate application build and artifact management.
