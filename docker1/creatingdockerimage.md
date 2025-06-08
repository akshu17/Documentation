
# How to Create a Docker Image from a Dockerfile

## 🐳 Step-by-Step Guide

### ✅ 1. Prepare Your Dockerfile
Make sure you have a `Dockerfile` in your working directory. Example:

```Dockerfile
# Dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

---

### ✅ 2. Open Terminal and Navigate to Project Directory

```bash
cd /path/to/your/project
```

---

### ✅ 3. Build the Docker Image

Use the `docker build` command with a tag name:

```bash
docker build -t my-python-app .
```

- `-t my-python-app`: Assigns a name (tag) to the image.
- `.`: Refers to the current directory (context) where the `Dockerfile` resides.

---

### ✅ 4. Verify the Image Was Created

```bash
docker images
```

You should see your image (`my-python-app`) listed.

---

### ✅ 5. Run a Container from the Image

```bash
docker run -p 5000:5000 my-python-app
```

This runs your image and maps port 5000 (or any relevant port).

---

## 📝 Optional Tips

- **Use `.dockerignore`** to exclude files/folders from the image build context.
- **Use tags** to version your images:  
  ```bash
  docker build -t my-python-app:v1.0 .
  ```
- **Rebuild after changes:**  
  ```bash
  docker build --no-cache -t my-python-app .
  ```
