# 安装证书管理

## 添加源

```bash
helm repo add jetstack https://charts.jetstack.io
```

## 更新 Repository

```bash
helm repo update
```

## 安装证书管理器

```bash
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --set installCRDs=true
```

## 卸载

```bash
helm --namespace cert-manager delete cert-manager
kubectl delete namespace cert-manager
```
