# OpenShift Study

Red Hat Developer Sandbox を利用して、OpenShift の基本操作を実践しました。

## 実施内容

- `oc` CLI を使ったOpenShiftの操作
- Deployment / Pod の作成
- ServiceによるPodへの接続
- Routeによる外部公開
- GitソースからNode.jsアプリをBuild / Deploy
- ブラウザからアプリへのアクセス確認

## nginxで発生したエラー

最初に通常の `nginx` イメージを使用したところ、Podが正常に起動せず、
以下の権限エラーが発生しました。

```text
mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
```

OpenShiftではコンテナを自由にroot権限で動かすのではなく、
セキュリティ上の制限がかかった状態で実行されることを実際に確認しました。

Podの設定を確認すると、`restricted-v2` SCCが適用され、
非rootユーザーで実行されていました。

そのため、非root実行に対応したイメージへ変更しました。

```text
nginxinc/nginx-unprivileged
```

変更後、Podが正常に起動しました。

## Routeによる外部公開

OpenShiftではServiceを作成しただけでは外部からアクセスできないため、
Routeを作成してブラウザからアクセスできるようにしました。

```text
Browser
  ↓
Route
  ↓
Service
  ↓
Pod
  ↓
Container
```

実際に触ることで、KubernetesのDeployment / Pod / Serviceをベースにしながら、
OpenShiftではRouteやSCCなどの仕組みが追加されていることを確認できました。

## マニフェスト

今回使用したnginxの設定をYAMLとして保存しています。

```text
nginx/
├── deployment.yaml
├── service.yaml
└── route.yaml
```