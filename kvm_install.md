## KVMのインストール
CentOS7 に KVM をインストールする手順。

### 必要なパッケージのインストール
```
# yum -y install qemu-kvm libvirt virt-install bridge-utils
```

### サービスの起動設定
```
# systemctl start libvirtd
# systemctl enable libvirtd
```

### ネットワークの設定
```
# nmcli connection add type bridge autoconnect yes con-name br0 ifname br0
# nmcli connection modify br0 ipv4.addresses <I/FのIP>/<subnetmask> ipv4.method manual
# nmcli connection modify br0 ipv4.gateway <gateway>
# nmcli connection modify br0 ipv4.dns <dns-server>
# nmcli connection delete <I/F名>
# nmcli connection add type bridge-slave autoconnect yes con-name <I/F名> ifname <I/F名> master br0
```