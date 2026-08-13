---
data: 2021-10-28 20:20
---

# 将 `MetalLB` 部署为 `Kubernetes` 服务的本地负载均衡器

> `bitnami/metallb` Chart 已下线, 现使用官方维护的 `metallb/metallb` Chart。同时 MetalLB 0.13 之后移除了 `configInline` 扁平配置方式, 改为使用 `IPAddressPool`、`L2Advertisement` 等 CRD 进行配置。

使用 `Helm` 部署 `MetalLB` 的非常简单。

```bash
helm repo add metallb https://metallb.github.io/metallb
helm repo update

helm install metallb metallb/metallb \
  --create-namespace \
  --namespace metallb-system
```

您现在应该已经为每个节点启动了一个控制器 `pod` 和一个 `speaker`。

```bash
NAME                                     READY   STATUS    RESTARTS   AGE
pod/metallb-speaker-78fnb                1/1     Running   0          59m
pod/metallb-controller-ccd4c76b6-7khwt   1/1     Running   0          59m

NAME                             DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/metallb-speaker   1         1         1       1            1           kubernetes.io/os=linux   59m

NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/metallb-controller   1/1     1            1           59m

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/metallb-controller-ccd4c76b6   1         1         1       59m
```

## 配置

安装完成后, 需要创建 `IPAddressPool` 和 `L2Advertisement` 资源来配置可分配的地址范围 (原 `configInline.address-pools` 的等价配置)。

```YAML
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: default
  namespace: metallb-system
spec:
  addresses:
    - 10.45.0.0/16
---
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: default
  namespace: metallb-system
spec:
  ipAddressPools:
    - default
```

```bash
kubectl apply -f ipaddresspool.yaml
```

让我们用 `helm` 部署一个 `NGINX` 来测试它。

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo update

helm upgrade --install \
    nginx bitnami/nginx \
    --set service.type=LoadBalancer \
    --namespace demo \
    --create-namespace
```

你会看到服务收到了来自 `MetalLB` 的 `External IP`

```bash
$ kubectl get service --namespace demo nginx

NAME        TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
nginx       LoadBalancer   10.43.47.65    10.0.100.0      80:31505/TCP   24s
```

您现在可以使用 `External IP` 和服务端口访问该服务

```bash
$ curl 10.0.100.0

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

等等, 如果需要清理演示环境

```bash
helm uninstall nginx --namespace demo
kubectl delete namespaces demo
```

## 参考

[ISSUES WITH K3S](https://metallb.universe.tf/configuration/k3s/)

[Installation With Helm](https://metallb.universe.tf/installation/#installation-with-helm)

[metallb/metallb - Installation With Helm](https://metallb.universe.tf/installation/#installation-with-helm)

[Configuration - IPAddressPool](https://metallb.universe.tf/configuration/#advertise-the-ip-pool)

[Make istio-ingress working with metallb bare metal kubernetes cluster](https://stackoverflow.com/questions/66623075/make-istio-ingress-working-with-metallb-bare-metal-kubernetes-cluster)

[Deploy MetalLB as an on prem load-balancer for your Kubernetes services](https://devops.cisel.ch/deploy-metallb-as-an-on-prem-load-balancer-for-your-kubernetes-services)

[安装 metallb 和 ingress](https://blog.linuxnb.com/index.php/post/178.html)

[k8s 使用 traefik 与 metallb 实现域名访问](https://www.cnblogs.com/bit-zjh/p/14818743.html)

[kuberntes 部署 metallb LoadBalancer](https://blog.csdn.net/networken/article/details/85928369)

[开源 k8slb 工具 Metallb](https://ysicing.me/posts/k8s-slb-metallb/)
