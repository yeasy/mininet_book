## 示例程序
Mininet 代码中带有了大量的示例程序，供大家参考和理解代码。所有的示例程序都在 example 目录下，包括
### baresshd.py:
使用 Mininet 的中层 API 来在一个 namespace 中创建主机、链路，并在主机上启动 sshd 进程，让用户可以登录。并未使用 OpenFlow。
### consoles.py:
为每一个节点都创建一些 console 窗口，并允许用户对这些节点进行操作和观测，支持图形界面。
### controllers.py:
使用一个自定义的Switch() 子类，创建一个带有多个控制器的网络。
### controllers2.py:
创建一个拥有多个控制器的网络，通过创建空的网络，添加节点和手动启动交换机实现。
### controlnet.py:
通过创建两个mininet对象来建模一个控制网络和数据网络。
###　cpu.py:
在不同的 CPU 限制下测试 iperf 的带宽性能。
### emptynet.py:
演示创建一个空的网络，之后添加节点进去。
### hwintf.py:
添加一个接口 （例如一个物理接口）到一个网络中。
### limit.py:
演示如何使用 link 和 CPU 限制。
### linearbandwidth.py:
基于 Topo 创建一个拓扑子类，并进行简单的测试。
### miniedit.py:
通过一个图形界面的编辑器来创建网络。
### multiping.py:
使用 node.monitor() 来检测多个主机的输出。
### multipoll.py:
检测多个主机的输出文件。
### multitest.py:
创建一个网络，并在其上进行多个测试。
### nat.py:
将 Mininet 的网络通过 nat 连接到外部网络中。
### popen.py:
使用 host.popen() 和 pmonitor() 来检测多个主机。
### popenpoll.py:
使用 node.popen() 和 pmonitor() 检测多个主机的输出。
### scratchnet.py, scratchnetuser.py:
使用底层的 Mininet 函数来创建网络。
### simpleperf.py:
配置网络和 CPU、带宽限制等。
### sshd.py:
在每个主机里面运行一个 sshd 进程，使得用户可以通过 ssh 来访问主机。这需要将 Mininet 的数据网络连接到 root 名字空间的一个接口上。一般的，控制网络已经在 root 名字空间了，所以默认已经被连接。
### tree1024.py:
创建一个 1024 主机的网络，然后运行 CLI。根据系统资源情况，可能需要利用 sysctl 进行相关修改。
### treeping64.py:
创建一个 64 主机的树状网络，利用 ping 来检查连通性。
