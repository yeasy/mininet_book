# 高级功能

本章将通过一个具体管理 Openflow switch 的例子来介绍一些比较高级的命令。

首先，启动 Mininet，执行
```
sudo mn --topo single,3 --mac --switch ovsk --controller remote
```
生成一个小的网络，三台主机连到一台交换机上，交换机为 OpenvSwitch 交换机，指定 remote 类型控制器（默认为本地）。
