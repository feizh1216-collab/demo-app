# Argo CD Demo App

这个仓库包含一个最小可用的 Argo CD 演示应用 `demo-nginx`。

## 目录结构

- `apps/demo-nginx/deployment.yaml`: Nginx Deployment（`nginx:1.25`）
- `apps/demo-nginx/service.yaml`: 对应 ClusterIP Service
- `argocd/application-demo-nginx.yaml`: Argo CD Application 清单

## 使用前修改

请先修改 `argocd/application-demo-nginx.yaml` 中的 `spec.source.repoURL`，改成你自己的 Git 仓库地址。

## 应用命令

```bash
kubectl apply -f apps/demo-nginx/deployment.yaml
kubectl apply -f apps/demo-nginx/service.yaml
kubectl apply -f argocd/application-demo-nginx.yaml
```

如果你已经登录 Argo CD CLI，也可以用：

```bash
argocd app create demo-nginx \
  --repo https://github.com/your-org/demo-app.git \
  --path apps/demo-nginx \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default

argocd app sync demo-nginx
argocd app get demo-nginx
```
