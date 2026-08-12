# 安装 NGINX Ingress

```bash
helm upgrade --install \
  nginx-ingress nginx/nginx-ingress \
  --create-namespace \
  --namespace nginx-ingress \
  --set service.spec.externalTrafficPolicy=Local
```

```bash
kubectl get all --namespace nginx-ingress
```

```bash
curl 10.0.100.1
```
