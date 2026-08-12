# 安装 Containerd

## 获取最新版本号

```bash
export CURRENT_CONTAINERD_VERSION=$(curl -sL https://api.github.com/repos/containerd/containerd/releases/latest | jq -r ".tag_name" | cut -c2-)
```

## 下载最新版本

```bash
wget https://github.com/containerd/containerd/releases/latest/download/cri-containerd-cni-${CURRENT_CONTAINERD_VERSION}-linux-amd64.tar.gz
```

## 安装

```bash
tar --no-overwrite-dir -C / -xzf cri-containerd-cni-${CURRENT_CONTAINERD_VERSION}-linux-amd64.tar.gz
```

## 生成配置

```bash
mkdir -p /etc/containerd
containerd config default > /etc/containerd/config.toml
```

## 启用服务

```bash
systemctl daemon-reload
```
## 启动

```bash
systemctl start containerd
```
