# 使用 Oracle Cloud 的免费层构建 Kubernetes (k3s) 集群

当谈到云托管时, Kubernetes 会很快变得昂贵, 特别是对于想要托管应用程序或进行一些个人开发的爱好者而言。

偶然发现了 Oracle 云免费层, 他们提供了“永远免费”的丰富资源。

这似乎是一个完美的机会, 可以让一个功能强大的始终免费的集群运行起来。

**OCI 免费实例:**

- AMD 实例: `2` 个

> 1 OCPU  
> 1GB RAM  
> 0.48Gbps Bandwidth  
> 46.6GB Boot Volume

- ARM 实例: `1-4` 个

> 共 `4 OCPU * 2.8 GHz Ampere Altra 80C` 资源  
> 最大 `24GB RAM`  
> 可以用做 1 个实例或最多 4 个实例  
> 出口带宽 1 OCPU = 1GB 最大 4GB

- 负载均衡器: `1` 个

> 带宽 `10 Mbps`。

- 每个月 `10TB` 出站数据。

- `2`个块卷存储, 总共 `200 GB`。

https://www.oracle.com/cloud/free/#always-free

> x86 CPU 架构(AMD 和 Intel)上的 1 个 OCPU = 2 个 vCPU；  
> Arm CPU 架构上的 1 个 OCPU = 1 个 vCPU

## 安装 `K3S`

```bash
curl -sfL https://get.k3s.io |  \
  K3S_NODE_NAME="master"   \
  K3S_KUBECONFIG_MODE="0644"   \
  K3S_KUBECONFIG_OUTPUT="/root/.kube/config"   \
  INSTALL_K3S_CHANNEL="latest"   \
  INSTALL_K3S_EXEC="--disable-cloud-controller --kube-controller-manager-arg cloud-provider=external --kubelet-arg cloud-provider=external --kubelet-arg provider-id=ocid1.instance.oc1.ap-chuncheon-1.an4w4ljrikpf5ayczg363a3mub2e37jxzx3hke67mj5svnn3fiaodexn5e3q --container-runtime-endpoint unix:///run/containerd/containerd.sock --no-deploy traefik,servicelb --tls-san $(curl -sSL ido.al)"   \
  sh -
```

curl -sfL https://get.k3s.io |  \
  K3S_NODE_NAME="master"   \
  K3S_KUBECONFIG_MODE="0644"   \
  K3S_KUBECONFIG_OUTPUT="/root/.kube/config"   \
  INSTALL_K3S_CHANNEL="latest"   \
  INSTALL_K3S_EXEC="--disable-cloud-controller --kube-controller-manager-arg cloud-provider=external --kubelet-arg cloud-provider=external --kubelet-arg provider-id=ocid1.instance.oc1.ap-chuncheon-1.an4w4ljrikpf5ayczg363a3mub2e37jxzx3hke67mj5svnn3fiaodexn5e3q --no-deploy traefik,servicelb --tls-san $(curl -sSL ido.al)"   \
  sh -

### 提示

```bash
apt install bash-completion

kubectl completion bash >/etc/bash_completion.d/kubectl

source /usr/share/bash-completion/bash_completion

source <(kubectl completion bash)

cat <<EOF > /root/.bashrc

# Bash Completion
# -----------------------------
source /usr/share/bash-completion/bash_completion

# Kubectl
# -----------------------------
alias k=kubectl
alias kc=kubectl
complete -F __start_kubectl k
complete -F __start_kubectl kc
EOF
```
