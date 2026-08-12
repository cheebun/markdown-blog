# Helm

## 安装

### 下载

```bash
wget https://get.helm.sh/helm-v3.7.1-linux-amd64.tar.gz
```

### 解压

```bash
tar \
  -zxvf helm-v3.7.1-linux-amd64.tar.gz \
  --strip-components=1 \
  linux-amd64/helm
```

### 添加权限

```bash
chmod +x helm
```

### 移动

```
mv helm /usr/local/bin
```

<br />
<br />

## 使用

### 添加常用源

```bash
helm repo add gitlab        https://charts.gitlab.io
helm repo add metallb      	https://metallb.github.io/metallb
helm repo add traefik      	https://containous.github.io/traefik-helm-chart
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
