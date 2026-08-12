# 离线安装

下载所需文件

```bash
wget https://raw.githubusercontent.com/k3s-io/k3s/master/install.sh
wget https://github.com/k3s-io/k3s/releases/download/v1.22.2%2Bk3s2/k3s
wget https://github.com/k3s-io/k3s/releases/download/v1.22.2%2Bk3s2/k3s-airgap-images-amd64.tar
```

复制镜像到指定目录

```bash
mkdir -p /var/lib/rancher/k3s/agent/images/
cp ./k3s-airgap-images-amd64.tar /var/lib/rancher/k3s/agent/images/
```

复制 `k3s` 到 `bin` 目录

```bash
cp ./k3s /usr/local/bin
chmod +x /usr/local/bin/k3s
```

执行安装脚本

```bash
K3S_NODE_NAME=master \
K3S_KUBECONFIG_MODE="644" \
K3S_KUBECONFIG_OUTPUT="/root/.kube/config" \
INSTALL_K3S_SKIP_DOWNLOAD=true \
INSTALL_K3S_CHANNEL=stable \
KUBE_PROXY_MODE="ipvs" \
INSTALL_K3S_EXEC="--no-deploy traefik --no-deploy servicelb" \
./install.sh
```

```bash
K3S_NODE_NAME="node" \
K3S_TOKEN="" \
K3S_URL="https://control-plane:6443" \
KUBE_PROXY_MODE="ipvs" \
INSTALL_K3S_SKIP_DOWNLOAD="true" \
INSTALL_K3S_CHANNEL="latest" \
./install.sh
```
