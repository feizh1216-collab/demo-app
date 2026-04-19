# AGENTS.md

## 项目目标
这个仓库用于管理 minikube 上的 Argo CD / Argo Rollouts 示例。

## 工作规则
- 所有变更优先修改 Git 仓库文件，不直接修改线上对象
- 默认使用 Kubernetes YAML，不引入 Helm，除非明确要求
- 新增资源时优先放到 apps/<app-name>/ 目录
- 改动后先执行 YAML 基本校验
- 不删除已有资源，除非我明确要求
- 任何涉及 Argo CD 的变更，优先生成 Application 清单
- 任何涉及灰度发布的变更，优先生成 Rollout 清单
- 所有说明写入 README.md
- 禁止执行 kubectl apply / kubectl delete / kubectl patch 到集群，除非我明确批准
- 对 Argo CD 的变更，默认只修改 argocd/*.yaml，不调用 argocd CLI 直接改线上应用