# 安装 v2ray

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  creationTimestamp: null
  name: v2ray
data:
  config.json: |
    {
      "inbounds": [
        {
          "tag": "VMess-WebSocket-In",
          "protocol": "vmess",
          "listen": "0.0.0.0",
          "port": 80,
          "settings": {
            "clients": [
              {
                "id": "04e09d0b-aaf9-41c0-9e06-879f5838c748",
                "email": "admin@microlove.me",
                "alterId": 0,
                "level": 0,
                "security": "none"
              }
            ]
          },
          "streamSettings": {
            "network": "ws",
            "security": "none",
            "wsSettings": {
              "acceptProxyProtocol": false,
              "path": "/"
            }
          }
        }
      ],

      "outbounds": [
        {
          "protocol": "freedom",
          "settings": {},
          "tag": "Proxy"
        },

        {
          "protocol": "freedom",
          "settings": {},
          "tag": "Direct"
        },

        {
          "protocol": "blackhole",
          "settings": {},
          "tag": "Reject"
        },

        {
          "protocol": "dns",
          "tag": "DNS-Out"
        }
      ],

      "dns": {
        "hosts": {
          "dns.google": "8.8.8.8",
          "doh.pub": "119.29.29.29"
        },

        "servers": [
          "https://dns.google/dns-query",
          {
            "address": "https+local://223.5.5.5/dns-query",
            "domains": ["geosite:cn", "geosite:icloud"],
            "expectIPs": ["geoip:cn"]
          },
          {
            "address": "https://1.1.1.1/dns-query",
            "domains": ["geosite:geolocation-!cn"]
          }
        ]
      },

      "routing": {
        "domainStrategy": "AsIs",
        "rules": [
          {
            "type": "field",
            "protocol": ["bittorrent"],
            "outboundTag": "Reject"
          },

          {
            "type": "field",
            "inboundTag": [
              "Http-In",
              "Https-In",
              "NpmpTrap-In",
              "HttpAlt-In",
              "VMess-WebSocket-In"
            ],
            "network": "udp",
            "port": 53,
            "outboundTag": "DNS-Out"
          },

          {
            "type": "field",
            "domain": [
              "geosite:tld-cn",
              "geosite:icloud",
              "geosite:cn",
              "geosite:private",
              "geosite:geolocation-cn"
            ],
            "outboundTag": "Direct"
          },

          {
            "type": "field",
            "ip": ["geoip:private", "geoip:cn"],
            "outboundTag": "Direct"
          },

          {
            "type": "field",
            "domain": ["geosite:geolocation-!cn"],
            "outboundTag": "Proxy"
          },

          {
            "type": "field",
            "network": "tcp,udp",
            "outboundTag": "Proxy"
          }
        ]
      }
    }

---
kind: Deployment
apiVersion: apps/v1
metadata:
  name: v2ray
spec:
  selector:
    matchLabels:
      app: v2ray
  template:
    metadata:
      labels:
        app: v2ray
    spec:
      containers:
        - name: v2ray
          image: zydou/v2ray
          ports:
            - containerPort: 80
          volumeMounts:
            - name: v2ray
              mountPath: /etc/v2ray/config.json
              subPath: config.json
      volumes:
        - name: v2ray
          configMap:
            name: v2ray

---
apiVersion: v1
kind: Service
metadata:
  name: v2ray
spec:
  selector:
    app: v2ray
  type: LoadBalancer
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30088

---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: v2ray
spec:
  ingressClassName: nginx
  rules:
    - host: 01.sea.usa.across.proxysite.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: v2ray
                port:
                  number: 80
```

```bash
kubectl apply -f v2ray.yaml --namespace website
```
