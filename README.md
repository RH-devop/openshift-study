\# OpenShift Study



Red Hat Developer Sandbox を利用して、OpenShift の基本操作と

Kubernetes との関係を実践形式で学習したリポジトリです。



\## 学習内容



\- OpenShift と Kubernetes の関係

\- Red Hat Developer Sandbox

\- Web Console

\- oc CLI

\- Project

\- Deployment / ReplicaSet / Pod

\- Service

\- Route

\- SCC（Security Context Constraints）

\- 非 root コンテナ

\- Operator の概念

\- Git ソースからのアプリケーション Build / Deploy

\- GitLab CI/CD と OpenShift の連携イメージ



\## nginx 構成



```text

Browser

&#x20; ↓

Route

&#x20; ↓

Service

&#x20; ↓

Deployment

&#x20; ↓

ReplicaSet

&#x20; ↓

Pod

&#x20; ↓

nginx-unprivileged Container

