
# 🐳 Container Crashes After `docker run -p` — Common Causes & Fixes

If your **container crashes immediately after running `docker run -p ...`**, it’s usually due to internal issues in the container — not the port mapping itself.

---

## 🔍 1. Check Logs
```bash
docker logs <container_id or name>
```
Often reveals crash cause like file errors, port mismatch, or missing dependencies.

---

## ⚙️ 2. Command or Entrypoint Is Wrong
If `CMD` or `ENTRYPOINT` in Dockerfile is incorrect, the container exits.

**Fix:**
Try running an interactive shell:
```bash
docker run -it myapp /bin/sh
```

Dockerfile example:
```dockerfile
CMD ["node", "app.js"]
```

---

## 🌐 3. App Not Listening on Correct Port
You expose `-p 8080:80`, but your app may not listen on port 80.

**Fix:**
Ensure your app listens on the right interface and port:
```python
# Flask example
app.run(host='0.0.0.0', port=80)
```

---

## 🔒 4. Missing Dependency or Permission Denied
App may crash due to missing files, packages, or insufficient permissions.

**Fix:**
Check volume mounts, permissions, and environment variables.

---

## 💥 5. No Long-Running Process
If the main process exits, so does the container.

**Fix:**
Ensure foreground execution in CMD:
```bash
CMD ["node", "server.js"]  # Not "node server.js &"
```

---

## 🧪 6. Debug with Interactive Mode
```bash
docker run -it --entrypoint /bin/sh myapp
```
Helps identify runtime issues manually.

---

## 🛠️ 7. Use Healthchecks and Restart Policy
```bash
docker run --restart=always \
  --health-cmd="curl -f http://localhost:80 || exit 1" \
  myapp
```

---

## ✅ Summary

| Issue | Symptom | Fix |
|-------|---------|-----|
| Wrong CMD | Immediate exit | Set proper long-running CMD |
| Wrong port | App unreachable | Match app port to `-p` |
| File missing | Crash logs | Use volumes correctly |
| Permissions | Denied errors | `RUN chown` or `USER` in Dockerfile |
