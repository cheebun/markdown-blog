# V2ray 离线安装

> 注意：v2ray-core 已由社区 fork 为 [v2fly/v2ray-core](https://github.com/v2fly/v2ray-core)（沿用原名，社区维护）与 [XTLS/Xray-core](https://github.com/XTLS/Xray-core)（性能与协议特性更激进的分支）两个生态。下方以 v2fly 版本为例，如需 Xray-core 请参考其官方安装脚本。

```bash
mkdir tmp && cd tmp

wget https://github.com/v2fly/v2ray-core/releases/download/v5.52.0/v2ray-linux-64.zip

unzip v2ray-linux-64.zip

mkdir -p /usr/local/etc/v2ray/

mkdir -p /usr/local/share/v2ray

mv ./systemd/system/v2ray.service /etc/systemd/system/v2ray.service

mv config.json /usr/local/etc/v2ray/

mv v2{ray,ctl} /usr/local/bin/

mv {geosite,geoip}.dat /usr/local/share/v2ray

cd .. && rm -r tmp

systemctl daemon-reload

systemctl enable v2ray

systemctl start v2ray
```
