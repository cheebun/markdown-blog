# Helm

## 安装

推荐使用官方安装脚本, 会自动获取最新版本 (撰写本文时为 `v4.2.3`)。

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod +x get_helm.sh
./get_helm.sh
```

> Helm v4 已于 2026 年成为当前稳定版, v3 仍在维护中 (Bug 修复至 2026-07-08, 安全修复至 2026-11-11)。如需手动下载指定版本, 可前往 [Helm Releases](https://github.com/helm/helm/releases) 查看。

<br />
<br />

## 使用

### 添加常用源

```bash
helm repo add gitlab        https://charts.gitlab.io
helm repo add metallb      	https://metallb.github.io/metallb
helm repo add traefik      	https://traefik.github.io/charts
helm repo add jetstack      https://charts.jetstack.io
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo add stable       	https://charts.helm.sh/stable
helm repo add nginx        	https://helm.nginx.com/stable
helm repo add bitnami      	https://charts.bitnami.com/bitnami
```

### 更新 Chart Repository

```bash
helm repo update
```
