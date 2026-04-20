# Argo CD Demo App

这个仓库包含一个最小可用的 Argo CD 演示应用 `demo-nginx`。

## 目录结构

- `apps/demo-nginx/rollout.yaml`: Argo Rollouts Rollout（`nginx:1.27`，canary 发布）
- `apps/demo-nginx/service.yaml`: 对应 ClusterIP Service
- `apps/demo-nginx/rollout-services.yaml`: Rollout 使用的 stable/canary Services
- `argocd/application-demo-nginx.yaml`: Argo CD Application 清单

## 说明

`demo-nginx` 现在使用 Argo Rollouts 进行灰度发布（canary）。
保留 `apps/demo-nginx/service.yaml` 作为统一访问入口，`rollout-services.yaml` 中的 stable/canary Service 由 Rollout 用于灰度阶段管理。

## 使用前修改

请先修改 `argocd/application-demo-nginx.yaml` 中的 `spec.source.repoURL`，改成你自己的 Git 仓库地址。

## 应用命令

```bash
kubectl apply -f apps/demo-nginx/rollout.yaml
kubectl apply -f apps/demo-nginx/service.yaml
kubectl apply -f apps/demo-nginx/rollout-services.yaml
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
