# Dockerfile Versioning

Dockerfile versioning isn’t a built-in Docker feature, but there are common ways and best practices to handle it effectively.

## What is Dockerfile versioning?

Dockerfile versioning means managing different versions of your Dockerfile over time so you can track changes, roll back if needed, and maintain multiple versions for different environments or features.

---

## Common ways to handle Dockerfile versioning:

### 1. Use Git (or any source control system)
- Store your Dockerfile(s) in a Git repository.
- Each commit represents a version change.
- Branches can be used for features or environments.
- Tags can mark releases or stable versions.
- This is by far the most common and recommended approach.

### 2. Multi-stage Dockerfiles with version-specific tags
- Use different tags in your Dockerfile `FROM` statements to pull specific base image versions.
- Build different image tags to represent versions, e.g., `myapp:v1.0`, `myapp:v1.1`.

### 3. Maintain multiple Dockerfiles
- For big changes or different environments, keep multiple Dockerfiles like:
  - `Dockerfile.dev`
  - `Dockerfile.prod`
  - `Dockerfile.v1`
  - `Dockerfile.v2`
- Specify which Dockerfile to use with `docker build -f Dockerfile.prod .`

### 4. Include version metadata inside the Dockerfile
- Add labels for version info:
  ```Dockerfile
  LABEL version="1.0"
  LABEL description="Initial release"
