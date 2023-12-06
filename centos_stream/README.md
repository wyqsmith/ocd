# CentOS Stream 9 虚拟化节点 の 初♂解禁

## 安装完成的环境说明

| 环境   | 值          |
|------|------------|
| 安装方式 | `minimal`  |
| 网络   | `DHCP`     |
| 新用户名 | `wyqsmith` |

## 安装完成后需要执行的一些操作

### 更新软件包（包含Kernel）

*PS: 当前用户为`root`*

```bash
dnf upgrade
```

（可选）如果此步骤包含内核更新，则重启系统，然后卸载旧内核。

```bash
rpm -qa | grep kernel
rpm -e kernel-***   # 旧内核包名
```

安装`vim`（自带的`vi`原生键位如果足够熟练的话，这步骤跳过就行）

```bash
dnf install vim
```

### 配置`sudo`并重启

```bash
usermod -aG wheel wyqsmith
reboot
```

### 配置网络

```bash
nmcli device
nmcli device show enp5s0
nmcli connection modify enp5s0 +ipv4.addresses 172.16.1.95
nmcli connection modify enp5s0 ipv4.method manual
nmcli connection modify enp5s0 ipv4.gateway 172.16.1.1
```

### 重启

### 必备软件

```bash
dnf install epel-release
dnf upgrade
dnf install wget lm_sensors smartmontools cockpit htop
```

## 虚拟机

### 安装KVM

```bash
dnf install qemu-kvm libvirt virt-install
```
