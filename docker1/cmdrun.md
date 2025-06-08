# Difference between CMD and RUN in Dockerfile

The difference between **CMD** and **RUN** primarily depends on the **context**—most commonly, this question arises in the context of **Dockerfiles**. Here's a breakdown:

---

### 🐳 In a Dockerfile:

#### **1. RUN**
- **Purpose:** Executes a command **at build time** to modify the image (e.g., install software, set up the environment).
- **Effect:** The result is **baked into the image** as a new layer.
- **Example:**
  ```dockerfile
  RUN apt-get update && apt-get install -y nginx
