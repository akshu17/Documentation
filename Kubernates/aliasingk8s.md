## ✅ `kubectl` Aliases Cheatsheet

### Basic alias

```bash
alias k='kubectl'
```

### Common get commands

```bash
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'
alias kgd='kubectl get deployments'
alias kgn='kubectl get nodes'
alias kgcm='kubectl get configmaps'
alias kgse='kubectl get secrets'
```

### Apply and delete

```bash
alias kaf='kubectl apply -f'
alias kdf='kubectl delete -f'
alias kdel='kubectl delete'
```

### Logs and exec

```bash
alias kl='kubectl logs'
alias kex='kubectl exec -it'
```

### Describe and edit

```bash
alias kd='kubectl describe'
alias ke='kubectl edit'
```

### Namespace shortcuts

```bash
alias kgns='kubectl get namespaces'
alias kcn='kubectl config set-context --current --namespace'
```

### Rollout operations

```bash
alias kru='kubectl rollout undo'
alias krs='kubectl rollout status'
alias krh='kubectl rollout history'
```

### Scale

```bash
alias ks='kubectl scale'
```

### Watch pods

```bash
alias kgpw='kubectl get pods --watch'
```

### Get all resources

```bash
alias kga='kubectl get all'
```

## 📌 How to use

1. Copy these aliases to your `~/.bashrc` or `~/.zshrc`
2. Reload your shell using `source ~/.bashrc` or `source ~/.zshrc`

## 🚀 Example usage

```bash
k get pods              # same as kubectl get pods
kgp                     # shortcut for kubectl get pods
kaf deployment.yaml     # apply YAML file
kl my-pod               # get logs of a pod
kex my-pod -- bash      # exec into a pod
```

