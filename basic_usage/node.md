## 对节点进行单独操作
如果想要对某个节点的虚拟机单独进行命令操作，也十分简单，命令格式为 `node cmd`。

例如查看交换机 s1 上的网络信息，我们只需要在执行的 ifconfig 命令前加上 s1 主机标志即可，即 `s1 ifconfig`，同样，如果我们想用 ping 3 个包的方法来测试 h2 跟 h3 之间连通情况，只需要执行 `h2 ping -c 3 h3` 即可。得到的结果为
```
mininet> h2 ping -c 3 h3
PING 10.0.0.3 (10.0.0.3) 56(84) bytes of data.
64 bytes from 10.0.0.3: icmp_seq=1 ttl=64 time=7.19 ms
64 bytes from 10.0.0.3: icmp_seq=2 ttl=64 time=0.239 ms
64 bytes from 10.0.0.3: icmp_seq=3 ttl=64 time=0.136 ms
— 10.0.0.3 ping statistics —
3 packets transmitted, 3 received, 0% packet loss, time 2006ms
rtt min/avg/max/mdev = 0.136/2.523/7.194/3.303 ms
```
在本操作执行后，可以通过 wireshark 记录查看到创建新的流表项的过程，这也是造成第一个 ping 得到的结果偏大的原因。

更简单的全网络互 ping 测试命令是 `pingall`，会自动所有主机节点逐对进行 ping 连通测试。

