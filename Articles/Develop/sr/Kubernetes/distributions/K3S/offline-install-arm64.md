## 离线安装 for ARM64

下载所需文件

```bash
wget https://raw.githubusercontent.com/k3s-io/k3s/master/install.sh
wget https://github.com/k3s-io/k3s/releases/download/v1.36.3%2Bk3s1/k3s-arm64 -O k3s
wget https://github.com/k3s-io/k3s/releases/download/v1.36.3%2Bk3s1/k3s-airgap-images-arm64.tar
```

> 版本请以 [k3s releases](https://github.com/k3s-io/k3s/releases) 页面为准, 此处以 `v1.36.3+k3s1` 为例。

复制镜像到指定目录

```bash
mkdir -p /var/lib/rancher/k3s/agent/images/
cp ./k3s-airgap-images-arm64.tar /var/lib/rancher/k3s/agent/images/
```

复制 `k3s` 到 `bin` 目录

```bash
cp ./k3s /usr/local/bin
chmod +x /usr/local/bin/k3s
```

执行安装脚本

服务端

```bash
K3S_NODE_NAME="master" \
K3S_KUBECONFIG_MODE="644" \
K3S_KUBECONFIG_OUTPUT="/root/.kube/config" \
KUBE_PROXY_MODE="ipvs" \
INSTALL_K3S_SKIP_DOWNLOAD="true" \
INSTALL_K3S_CHANNEL="latest" \
INSTALL_K3S_EXEC="--disable=traefik --disable=servicelb" \
./install.sh
```

> `--no-deploy` 参数已在 k3s v1.24 中移除, 现使用 `--disable` 替代。

```bash
K3S_NODE_NAME="node" \
K3S_TOKEN="" \
K3S_URL="https://control-plane:6443" \
KUBE_PROXY_MODE="ipvs" \
INSTALL_K3S_SKIP_DOWNLOAD="true" \
INSTALL_K3S_CHANNEL="latest" \
./install.sh
```
