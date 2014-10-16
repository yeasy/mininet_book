## 安装

### 使用镜像
#### 下载
官方网站已经提供了配置好相关环境的基于 Debian Lenny 的虚拟机镜像，下载地址为[http://openflowswitch.org/downloads/OpenFlowTutorial-081910.vmware.zip](http://openflowswitch.org/downloads/OpenFlowTutorial-081910.vmware.zip)， 压缩包大小为 700 MB 左右，解压后大小为 2.1 GB 左右。虚拟机镜像格式为 Vmware 的 vmdk，可以直接使用 vmware workstation 或者 Virtualbox 等软件打开。如果使用 QEMU 和 KVM 则需要先进行格式转换。

如果使用 Virtualbox 进行加载，需要注意
尽量使用最新版本，host 操作系统需要支持 PAE，并在 Virtualbox 中打开 PAE 支持。

#### 使用
默认用户名密码均为 openflow，建议通过本地利用 ssh 登录到虚拟机上使用（可以设置自动登录并将 X 重定向到本地），比较方便操作。

注意事项：
建议将 guest 主机采用 bridge 方式联网，以获取 host 可见的独立 IP；也可采用为 guest 配置两块网卡方式，一块采用 NAT（一般来说，guest 上看到为 eth0，IP 地址为 `10.0.2.*`，网关为 `10.0.2.2`），一块采用 host-only（guest 上的 eth1，IP 地址为`192.168.56.*`），但 host-only 的网卡可能无法自动 dhcp 到地址，需要手动配置（`ifconfig eth1 ip/mask`）将 host 机 .ssh 目录下 id_rsa.pub 复制到 guest 机的 .ssh 目录下，并写入 authorized_keys，可实现自动登陆认证。


### 本地安装
大部分发行版中已经带有该软件包，直接通过命令安装即可。例如，在 Ubuntu 系统中，执行

```
$ sudo aptitude install -y mininet
```

也可以通过源代码安装。
```
$ git clone https://github.com/mininet/mininet.git
$ cd mininet
```
参考 INSTALL 文件中针对不同操作系统的安装步骤。
