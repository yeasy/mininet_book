## 使用 dpctl
执行
```
dpctl show tcp:127.0.0.1:6634
```
可以查看到交换机的端口等基本情况，其中 tcp 端口 6634 是默认的交换机监听端口。

执行
```
dpctl dump-flows tcp:127.0.0.1:6634
```
可以看到更详细的流表信息。
此时，流表为空，执行 `h2 ping h3` 无法得到响应。因此我们需要通过 dpctl 手动添加流表项，实现转发。
命令为
```
dpctl add-flow tcp:127.0.0.1:6634 in_port=1,actions=output:2
dpctl add-flow tcp:127.0.0.1:6634 in_port=2,actions=output:1
```
此时查看流表可以看到新的转发信息，同时可以在 h2 和 h3 之间 ping 通。

## 使用ovs-ofctl
执行
```
sh ovs-ofctl add-flow s1 action=normal
```
将交换机s1的转发行为设置为normal，流表将会自动更新。

执行
```
sh ovs-ofctl del-flows s1
```
将交换机s1的流表清空。


我们可以自定义在不同网络层之间的流匹配。

执行
```
sh ovs-ofctl add-flow s1 priority=500, in_port=1, actions=output:2
sh ovs-ofctl add-flow s1 priority=500, in_port=2, actions=output:1
```
自定义第一层的流匹配规则，根据port进行匹配。

执行
```
sh ovs-ofctl add-flow s1 dl_src=00:00:00:00:00:01, dl_dst=00:00:00:00:00:02, actions=output:2
sh ovs-ofctl add-flow s1 dl_src=00:00:00:00:00:02, dl_dst=00:00:00:00:00:01, actions=output:1
sh ovs-ofctl add-flow s1 dl_type=0x806,nw_proto=1,actions=flood
```
自定义第二层的流匹配规则，根据协议和mac地址进行匹配。

执行
```
sh ovs-ofctl add-flow s1 priority=500, dl_type=0x800, nw_src=10.0.0.0/24, nw_dst=10.0.0.0/24, actions=normal
sh ovs-ofctl add-flow s1 priority=800, ip,nw_src=10.0.0.3,actions=mod_nw_tos:184,normal

sh ovs-ofctl add-flow s1 arp,nw_dst=10.0.0.1,actions=output:1
sh ovs-ofctl add-flow s1 arp,nw_dst=10.0.0.2,actions=output:2
sh ovs-ofctl add-flow s1 arp,nw_dst=10.0.0.3,actions=output:3
```
自定义第三层的流匹配规则，根据协议和IP地址进行匹配。

执行
```
h3 python -m SimpleHTTPServer 80 &
sh ovs-ofctl add-flow s1 arp,actions=normal
sh ovs-ofctl add-flow s1 priority=500,dl_type=0x800,nw_proto=6,tp_dst=80,actions=output:3
sh ovs-ofctl add-flow s1 priority=800,ip,nw_src=10.0.0.3,actions=normal
h1 curl h3
h2 curl h3
```
自定义第四层的流匹配规则。
