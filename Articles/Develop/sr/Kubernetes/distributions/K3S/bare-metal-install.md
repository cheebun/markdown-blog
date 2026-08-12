# 裸机安装

## 软件实现方案 (MetalLB)

假设我们 public ip 为 `1.1.1.1`。

### 配置 MetalLB

```bash
cat << EOF > metallb-values.yaml
configInline:
  address-pools:
    - name: public
      protocol: layer2
      addresses:
        - 1.1.1.1/32
    - name: default
      protocol: layer2
      addresses:
        - 10.45.0.0/16
EOF
```

### 安装 MetalLB

```bash
helm install \
  metallb metallb/metallb \
  --create-namespace \
  --namespace metallb-system \
  --values metallb-values.yaml
```

### 配置 Nginx Ingress

```bash
cat <<EOF > nginx-values.yaml
controller:
  healthStatus: true
  healthStatusURI: "/healthz"

  service:
    loadBalancerIP: 45.142.157.110
    externalTrafficPolicy: Local
    annotations:
      metallb.universe.tf/address-pool: public
EOF
```

### 安装 Nginx Ingress

```bash
helm install \
  nginx-ingress nginx/nginx-ingress \
  --create-namespace \
  --namespace nginx-ingress \
  --values nginx-values.yaml
```

## 通过主机网络 (DaemonSet + hostNetwork)

### 安装 Nginx Ingress

```bash
helm upgrade --install \
  nginx-ingress nginx/nginx-ingress \
  --create-namespace \
  --namespace nginx-ingress \
  --set controller.healthStatus=true \
  --set controller.healthStatusURI="/healthz" \
  --set controller.kind=daemonset \
  --set controller.hostNetwork=true \
  --set controller.service.create=false \
```
