# 安装 ETCD

export CURRENT_ETCD_VERSION=$(curl -sL https://api.github.com/repos/etcd-io/etcd/releases/latest | jq -r ".tag_name" | cut -c2-)

rm -rf etcd-v${CURRENT_ETCD_VERSION}-linux-amd64.tar.gz

wget https://github.com/etcd-io/etcd/releases/latest/download/etcd-v${CURRENT_ETCD_VERSION}-linux-amd64.tar.gz

tar -xzf etcd-v${CURRENT_ETCD_VERSION}-linux-amd64.tar.gz

mv etcd-v${CURRENT_ETCD_VERSION}-linux-amd64/etcd{,{c,u}tl} /usr/bin/

wget https://github.com/etcd-io/etcd/raw/main/contrib/systemd/etcd.service

mv etcd.service /etc/systemd/system/

groupadd --system etcd

useradd -s /sbin/nologin --system -g etcd etcd

mkdir /var/lib/etcd/

chown -R etcd:etcd /var/lib/etcd/

rm -rf etcd-v${CURRENT_ETCD_VERSION}-linux-amd64 etcd-v${CURRENT_ETCD_VERSION}-linux-amd64.tar.gz

systemctl daemon-reload

systemctl start etcd
