
# 🐳 Multi-Stage Dockerfile Example (Node.js App)

## ✅ Why Use Multi-Stage Builds?

Multi-stage builds help to:

- ✅ Separate build environment from runtime
- ✅ Minimize final image size
- ✅ Improve security (only copy what you need)

---

## 📦 Dockerfile

```dockerfile
# === Stage 1: Build stage ===
FROM node:20 AS builder

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy application source
COPY . .

# Optional: Build the app (for React/Next.js, etc.)
# RUN npm run build

# === Stage 2: Runtime stage ===
FROM node:20-slim

WORKDIR /app

# Only copy necessary files from the builder stage
COPY --from=builder /app .

# Expose the app's port
EXPOSE 3000

# Start the app
CMD ["node", "index.js"]
```

---

## 📁 Project Structure

```
my-node-app/
├── Dockerfile
├── package.json
├── package-lock.json
└── index.js
```

---

## 💡 Example `index.js`

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.end("Hello from multi-stage Docker image!");
});

server.listen(3000, () => console.log("Server running on port 3000"));
```

---

## 🏗️ Build and Run

```bash
# Build the Docker image
docker build -t yourname/multi-stage-node .

# Run the container
docker run -p 3000:3000 yourname/multi-stage-node
```

Visit `http://localhost:3000` in your browser to see the output.

---

## 🔍 Comparison Table

| Without Multi-Stage             | With Multi-Stage                   |
|--------------------------------|------------------------------------|
| Big final image                | Small final image                  |
| Dev tools & build files inside | Clean runtime-only environment     |
| Possible security risk         | Reduced attack surface             |

---

Let me know if you'd like:
- A Python or Java version of this example
- A downloadable project ZIP
- Docker Compose integration
