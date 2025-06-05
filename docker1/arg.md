# 🐳 ARG in Docker

## 📘 What is `ARG`?

`ARG` is a Dockerfile instruction used to define **build-time variables**. These variables are available **only during the image build** process, and not inside the running container (unless passed into `ENV`).

---

## 🛠️ Syntax

```dockerfile
ARG <variable_name>[=<default_value>]
Example 1: Using ARG with Default Value

Dockerfile:
FROM alpine
ARG APP_VERSION=1.0
RUN echo "Building app version $APP_VERSION"
Build Command:
docker build -t myapp .
Output:
Building app version 1.0
🧪 Example 2: Overriding ARG During Build

Build Command with Override:
docker build -t myapp --build-arg APP_VERSION=2.5 .
Output:
Building app version 2.5
🧪 Example 3: Using ARG to Set ENV

FROM ubuntu
ARG USER_NAME
ENV USER_NAME=${USER_NAME}
RUN echo "Container user is $USER_NAME"
Build:
docker build -t testimage --build-arg USER_NAME=admin .
Run:
docker run testimage
# Output: Container user is admin
Here, we pass the ARG into ENV so it's available at runtime too.

🧠 Key Points

Feature	Details
Scope	Build-time only
Overridable	✅ Yes, using --build-arg
Default Value	✅ Optional
Runtime Availability	❌ No, unless passed into ENV
Use Case	Customize build without hardcoding values
