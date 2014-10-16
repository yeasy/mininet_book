## 交换机类
### mininet.node.Switch
表示一个交换机的基类。

运行在 root 名字空间。主要包括 dpid、listenport 等属性。

### mininet.node.IVSSwitch
表示一台 indigo 交换机（需要系统中已存在）。

### mininet.node.OVSLegacyKernelSwitch
传统的 openvswitch 交换机，基于 ovs-openflowd。不推荐。

### mininet.node.OVSSwitch
表示一台 openvswitch 交换机（需要系统中已经安装并配置好 openvswitch），基于 ovs-vsctl 进行操作。目前所谓的 OVSKernelSwitch 实际上就是 OVSSwitch

### mininet.node.UserSwitch
用户态的 openflow 参考交换机，即 ofdatapath。不推荐。
